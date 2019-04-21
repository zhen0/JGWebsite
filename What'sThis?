## Mummy, What's This?  
### The Surprisingly Similar Steps To Identify "This" In Javascript And The World Of A Toddler.

I learned Javascript at around the same time as my daughter learned to talk.  So we both learned the power and confusion of ‘this’ at around the same time.  Figuring out what my daughter meant by this when she asked “what’s this?”  (about two hundred times an hour!) helped me understand better the process I could go through to figure what “this” is in javascript too.  Hopefully they can help you too!

### What is this?

In toddler world, “this” can be anything in my toddler’s field of vision.  It’s usually an object she likes the look of. 

In javascript, “this” also refers to an object.  But of course, a javascript one.  The biggest object in (browser-side) javascript is the window.  But ‘this’ can also refer to a specific object of your own creation. What it’s referring to all depends on the context. 

### Execution Context and Implicit Binding

When figuring out what my toddler’s ‘this’ is, I need to look at where she is and what she can see.  I also need to check if she has anything in her hand. This can help me figure out the context of her “what’s this” request and eventually work out what she’s asking about.  For example, if she’s at the dinner table, the context is dining and she’s likely asking about food. If we’re in the park and she’s holding a leaf, the context is that leaf. 

Execution Context in javascript is a similar thing.  To work out what “this” is I need to check where it is invoked.  If it is inside of an object (for example as part of a method), ‘this’ refers to that object. The object is its execution context. Equally if it’s outside of an object, the context is usually the global object, (which for browser side javascript is) the window.

### The Power of the Dot

Just as sometimes my daughter might ask ‘what’s this?” about a leaf and I could answer “it’s part of a tree”, so in javascript you can see the “this” of value as what it’s a bigger part of. A great step is to see if there is a dot in front of that value. 

For example, my daughter’s leaf could be tree.leaf in javascript, which would tell me the leaf belongs to the tree.  It’s “this” is the object “tree”.  Or NYC.Manhattan would show that Manhattan is part of NYC.  NYC is to the left of the dot so we know that the “this” of Manhattan is NYC. If there is no dot, the “this” is the global object (which for browser side javascript is) the window. 

### What about functions?

Unless we have engaged strict mode, (although it sounds like it, strict mode is not a parenting style - more info on it here!) “this” in a function is the global object. We can use special methods such as “call”, “apply” and “bind” to explicitly bind an object to a function and set its “this” to be the object we bind it to.  This is where the toddler comparison fails as I’ve yet to come up with a way to set my daughter’s context.   But there are some great resources to find out more about this and explicit binding here. 
