# **Simple Scheduling - How I used Prefect to remove the hassle of meal prep**

Prepping meals is fun. Planning meals is not. But not planning meals is even worse—and scrambling to cook chicken nuggets or waiting for takeout to be delivered leads to a grumpy, not exactly well-fed family. When I'm organized I create a weekly meal plan, get everything delivered ahead of time and know exactly what we'll be eating each night. However that planning takes an annoying amount of time and focus.

I decided there are better things to do with my time. So I did what any reasonable person would do: I automated it.

## **Choosing the Tools**

I could have just used Claude manually and added ingredients by hand. But I wanted something that ran itself every Saturday without me remembering. That's where Prefect came in.

I chose it because it lets me schedule and run code remotely without managing servers or dealing with infrastructure. The pythonic interface meant I could write normal Python—just decorators and functions—without wrestling with YAML configs or visual workflows. Prefect gives me built-in observability so I can see exactly what happened at each step. Retries happen automatically with exponential backoff, so when Claude times out or the MCP server hiccups, the workflow just recovers on its own.

What sealed it for me was how naturally it handles dynamic workflows. If the user provides feedback, I just write a normal Python `if` statement to regenerate and re-post to Slack. It's not special or complicated—it's just code. I added Pydantic Logfire on top to see deeper into what Claude is actually doing: token usage, API latency, user behavior patterns. Between Prefect's monitoring and Logfire's tracing, I have real visibility into whether this system is working.

## **Building It**

The workflow breaks into tasks: parse natural language dietary preferences into JSON, call Claude to generate two meals under 20 minutes with ingredient overlap, post to Slack, wait for approval/feedback, optionally regenerate, then add ingredients to Todoist via the hosted MCP server. I used Claude Code to generate the initial structure, then tuned the prompts. 

When I hit issues with the Todoist integration, I used the Prefect MCP to help debug—it turned out I had the wrong API key. The MCP helped me identify this by reading my flow run logs directly. It also helped me draft parts of the core flow logic initially, which saved me from having to switch back and forth to the docs while learning Prefect-specific elements like variable handling.

Prefect's task decorators made this straightforward to build:

```python
@task(
    name="parse_preferences",
    retries=2,
    retry_delay_seconds=10,
    persist_result=True,
)
async def parse_preferences_task(preferences_text: str) -> DietaryPreferences:
    """Parse dietary preferences from natural language."""
    with logfire.span("task:parse_preferences"):
        return await parse_dietary_preferences(preferences_text)
```

For the Claude integration, I wrapped Pydantic AI agents with PrefectAgent for durable execution with automatic retries:

```python
# Wrap with PrefectAgent for durable execution
prefect_agent = PrefectAgent(
    agent,
    model_task_config=TaskConfig(
        retries=2,
        retry_delay_seconds=[10.0, 20.0],
        timeout_seconds=60.0,
    ),
)
```

The feedback handling is just normal Python—no special workflow syntax needed:

```python
# Check approval status
if approval_input.approved:
    approval_received = True
    logfire.info("Meal plan approved")

elif approval_input.regenerate and approval_input.feedback:
    # User provided feedback, regenerate
    feedback_text = approval_input.feedback
    regeneration_count += 1
    logfire.info("Regenerating meal plan with feedback",
                 feedback=feedback_text)
```

The key prompts are straightforward. One parses preferences: *"vegetarian, no mushrooms, Mediterranean flavors, quick stir-fries"* becomes structured JSON. Another generates meals: given those preferences, create two different recipes that share 4-6 ingredients to reduce shopping list friction. The Prefect flow orchestrates these tasks, handles retries if Claude times out, and manages the state persistence around the approval gate. I scheduled it to run Saturday at 5 PM using Prefect Cloud's managed execution.

## **Next Steps**

I'm planning a few improvements. First, integrate AnyList instead of Todoist for ingredients—AnyList connects directly to online grocery delivery services, so approved meals flow straight into my shopping workflow without manual copying. Second, use a recipe MCP tool to give Claude access to a broader recipe database and real-time ingredient availability. Third, set up a second schedule for my husband so he can plan his weeks too, running Friday evenings so we can coordinate around each other's preferences.

The code is on GitHub: [github.com/zhen0/meal-planning-agent](https://github.com/zhen0/meal-planning-agent). If you're dealing with similar cognitive load around routine tasks, automation might be worth the effort—not necessarily to save time, but to reclaim mental space for things that actually matter.
