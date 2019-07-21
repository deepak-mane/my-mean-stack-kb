# Observable Usage: 

## How to use Interval in Angualar
```
import { Component, OnInit, OnDestroy } from '@angular/core';
import { interval, Subscription, Observable } from "rxjs";

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})

export class HomeComponent implements OnInit, OnDestroy {

  private firstObsSubscription: Subscription;
  constructor() { }
  
ngOnInit() {
    // Method:1 [Default,Delivered]
    // this.firstObsSubscription = interval(1000).subscribe(count => {
    //   console.log(count);
    // });

    // Method:2 [ Customized ]
    const customIntervalObservable = Observable.create(observer => {
      let count = 0;
      setInterval(() => {
          observer.next(count);
          if (count == 2) {
            observer.complete();
          }
          if (count > 3) {
            observer.error(new Error('Count is greater than 3'));
          }
          count++;
        }, 1000);
    });

    this.firstObsSubscription = customIntervalObservable.subscribe(data => {
      console.log(data);
    }, error => {
      console.log(error);
      alert(error.message);
    }, () => {
      console.log('Completed!');
    });
  }

  ngOnDestroy(): void {
    this.firstObsSubscription.unsubscribe();
  }
  ```


That was a lot of talking about observable balls but now we have an example of an observable and how it behaves under the hood.However I know that this can look even more confusing and you might ask yourself Well when do I write this code.

Because that's nice about the interval but come on I don't need that interval at all.In my application and you would be right and by the way if you needed one you'd of course use the built in interval function and not build your own one.

So what's the idea behind that example.
The idea is that you understand what happens inside of an observable whenever you subscribe and you set up your different handler functions here are extraneous in the end merges them all together into one object and passes that object the observer to the observable and inside of the observable it will then interact with the Observer and let the observer know about new data and errors and zone.

And that is how your functions get called.
However you rarely very very very rarely Build Your Own observable. More often you use observable that come with libraries like angular like the proud parents observable we already used under the hood that in the end is a custom observable built by the angular team but of course you just use it like that.

You rarely build your own ones but still it's super important to understand how they work under the hood and in the end they all work a bit like that. They wrap some event sauce. In this case it's set interval.

In other cases it could be an ajax request or a click listener or whatever it is and they give you data or possibly also errors or the complete event and you will mostly use subscribe and pass and functions that deal with that data or those errors.
### END 
