# Angular-Observables-Observers-Subscriptions

![alt text](./images/Angular-Observables-Observers-Subscriptions.png)


# What's this observable? 

As you could probably tell by the code we wrote, it's all about us emitting data and listening to that data in different places of our application which makes it pretty helpful because we can well subscribe to certain updates, changes and push these changes from a totally different place, here's more theory on that.

So we typically think in observables and observers, the observer is essentially the thing subscribing to an observable or the thing which establishes the subscription and manages it you could say. There are three methods which are called on the observers side and that's next, error and complete.

Now we called next on the subject in the last lectures and the subject is kind of the observable you could say but it's the observer who then does something upon the next call in that subscription callback we passed right, that first argument we passed to subscribe, that is the logic we want to execute whenever next is executed on the subject to to say.

So we invoke next through the observable or through the subject, I'll come to the difference and the observer is what we basically pass into subscribe, so it's a collection of functions that can do something up on these method calls. And as I also explained briefly, we can not just emit next data, so a new package of data so to say, we could also  have an observable where we want to throw an error, maybe because we are doing some http calls behind the scenes that failed or we could also emit a complete event to basically say hey I'm done, there are no more data packages to be emitted, so no more next calls.

Now a typical example but of course not limited to that is an observable  that wraps a callback of an http request, so we could wrap a normal xml http request and ajax request with an observable that basically takes that callback and whenever that request gives us back a response, we instead use that observable to emit the response data or a possible error as a next or error message. 

And that is essentially what we could do, we could also complete the observable once the response is there because of course if the response is there, this http request will not yield any responses, as I said it could also fail and that is how we could manage such a http request. Now in our app,  we didn't manage an http request though, we managed a subject or our own event emitter therefore. Now a subject is really just a special kind of observable, a normal observable is kind of passive, you wrap a callback or an event source like a click listener with it. So you don't actively trigger when a new data package is emitted, that happens when your http requests gets a response or when the user clicks something, instead you just yeah well set up this listener and then you can subscribe to it. A subject is more active, we also subscribe to a subject but there we can manually call next and that makes it a perfect event emitter because we cannot just subscribe and wait for something which we can't directly influence instead we can directly influence when a new data package is emitted and that's exactly what we need in our application.

When we add a new post, then we actively want to notify our entire application  and that is what we can do with a subject. So in general, you can think of observables and therefore also subjects as streams of data or of values, so we've got one value and we can have more values which are emitted over time depending on the observable  and the data source it covers. Then we have the observer, so that's essentially this set of functions we can call, next, error and complete and for a normal value, we typically would call next and if we have an observable that wraps something like a http request, then it would do that for us and as I said we can have more than one value over the course of our application, that depends on how we were using that observable. 

Eventually it may end but of course there are also observables that may never end, for example if you're wrapping a normal click listener with it, well then this will typically never end, if you've got an observable that ends, well then the complete function will be called.

And this is how it works, this is how we work with observables, how we should think about them, if you want to learn way more about rxjs observables, in the last lecture of this module, you'll find a link to an in-depth series I created on YouTube but that's the core mental model to wrap your head around for now. We will mostly use the subject, we will indirectly use some observables and I will explain what they do when we use them  but in the end think of it as a stream of data which you can actively manage in the case of a subject or which is managed for you if you are wrapping some well source who can directly influence and then you can decide what you want to do when new data is emitted in your subscription.

So now with this closer look at observables, let's finish up our form here on the angular frontend and do some first polishing before we move to the backend and add node so that we don't just have a frontend  but we also start working on the backend.

### ****************************************
