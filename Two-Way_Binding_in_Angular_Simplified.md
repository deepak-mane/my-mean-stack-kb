

# Simplifying Custom Two-Way Data Binding in Angular
- Dhananjay Kumar / Monday, December 12, 2016

There are three types of data bindings in Angular , they are as follows:

1. Interpolation
2. Event Binding
3. Property Binding

If you are coming from an Angular 1.X background, you might be wondering that where is the two-way data binding? Remember, the first time you saw AngularJS 1.X demo and you were just blown away the by power of ng-model? Yes, like you, I was also very impressed by power of two-way data binding in AngularJS 1. Even though, AngularJS 1 two-way data binding was beautiful, it came with the baggage of digest cycle and $watch.

To simplify the things, Angular  does not have any built in Two-Way data binding. It does not mean; you cannot have two-way data binding in Angular application. Come on, we cannot think of creating a modern web application without having power of two-way data binding. So, in this post, we are going to learn, how to work with two-way data binding in Angular 

## Two-way data binding with ngModel

Angular  provides us a directive ngModel to achieve two-way data binding. It is very simple and straight forward to use ngModel directive as shown in the listing below:
```
import {Component} from '@angular/core';

@Component({
    moduleId:module.id,
    selector:'my-app',
    template:`
  <div class="container">
     <input [(ngModel)]='name' />
      <br/>
      <h1>Hello {{name}}</h1>
  </div>
  `
})
export class AppComponent{

}
```

To use ngModel directive, we need to import FormsModule in the application. For your reference, below I am listing app.module.ts  which is importing FormsModule besides other required modules.
```
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule }   from '@angular/forms';

import { AppComponent }  from './app.component';

@NgModule({
    imports:      [ BrowserModule,FormsModule ],
    declarations: [ AppComponent],
    bootstrap:    [ AppComponent ]
})
export class AppModule { }
```
In above demo, when typing into the input element, the input’s value will be assigned to name variable and also it would be displayed back to the view. So we are implementing two-way data binding using ngModel as shown in the below image:

## Two-way data binding without ngModel

To understand ngModel directive working, let us see how we can achieve two-way data binding without using ngModel directive. To do that, we need to use

Property binding to bind expression to value property of the input element. In this demo, we are binding name variable expression to value property.  
Event binding to emit input event on the input element. Yes, there is an input event which will be fired whenever user will input to the input element. Using event binding, input event would be bind to an expression.
So, using the property binding and the event binding, two-way data binding can be achieved as shown in the listing below:
```
import {Component} from '@angular/core';

@Component({
    moduleId:module.id,
    selector:'my-app',
    template:`
  <div class="container">
     <input [value]="name" (input)="name=$event.target.value" />
      <br/>
      <h1>Hello {{name}}</h1>
  </div>
  `
})
export class AppComponent{

        name : string = "";
    }
```
Same like ngModel directive demo in this demo also, when typing into the input element, the input element’s value will be assigned to name variable and also it would be displayed back to the view.

So we are implementing two-way data binding without using ngModel using the code shown in the below image:

 

 Let us understand few important things here:

1. [value]=”name” is the property binding. We are binding value property of the input element with variable (or expression) name.
2. (input)= “expression” is event binding. Whenever input event will be fired expression will be executed.
3. “name=$event.target.value” is an expression which assigns entered value to name variable.

## Name variable can be accessed inside AppComponent class.
 So far we have seen two-way data binding using ngModel and without ngModel. We can conclude that the directive ngModel is nothing but a combination of property binding and event binding. Event binding is denoted using small bracket and property binding is denoted using square [] bracket, and if you notice syntax of ngModel is [(ngModel)], which is like a banana put into a box suggests it is combination of both event and property binding.


## Custom two-way data binding

We should be very careful whether to create a custom two-way data binding or rely on the ngModel directive. We really don’t have to create custom two-way data binding always. However, it is good to know steps to create a custom two-way data binding. Let us create a customcounter component with two-way data binding enabled. Let us follow the steps:

  - Step 1

Create a component with two buttons and methods to increment and decrement.  
```
@Component({
    moduleId: module.id,
    selector:'countercomponent',
    template:`
    <button (click)='increnent()'>Increment</button>
    {{count}}
    <button (click)='decrement()'>Decrement</button>
    `
})
export class  AppChildComponent {

        count : number = 0;      
        increment(){

            this.count = this.count+1; 
        }

        decrement(){
            this.count = this.count - 1; 
        }
    }
```    
Above we have created a very simple component to increment and decrement the count. Now very much we can use this component inside another component, however, two-way data binding is not enabled on this component.  To enable that, we need to use @Input and @Output properties.

  - Step 2

Let us create a getter with @Input() property. This getter will return the count. Since it is attributed to @Input() decorator, consumer of this component can bind this value using the property binding.
```
@Input() 
    get counter(){

        return this.count; 
    }
 ```

  - Step 3

To create two-way data binding, we need to create an event of the type EventEmitter. This event is attributed to @Output() decorator such that it can be emitted to the consumer component. We are creating event object in the constructor of the component.
```
@Output() counterChange :  EventEmitter<number>;
    constructor(){
         
        this.counterChange = new EventEmitter();
         
    }
 
```
  - Step 4

As the last step, increment and decrement functions should emit the counterChange event. So, we need to modify increment and decrement function as shown in the listing below:
```
   increment(){

        this.count = this.count+1; 
        this.counterChange.emit(this.count);
    }

    decrement(){
        this.count = this.count - 1; 
        this.counterChange.emit(this.count);
    }
```    
Both functions are emitting the counterChange event. Putting every piece together, a component with custom two-way data binding will look like code listed below:
```
import {Component,Input,Output,EventEmitter} from '@angular/core';

@Component({
    moduleId: module.id,
    selector:'countercomponent',
    template:`
    <button (click)='increment()'>Increment</button>
    {{count}}
    <button (click)='decrement()'>Decrement</button>
    `
})
export class  AppChildComponent {

        count : number = 0;   

     @Output() counterChange :  EventEmitter<number>;
        constructor(){
         
            this.counterChange = new EventEmitter();
         
        }
     
     @Input() 
        get counter(){

            return this.count; 
        }

        increment(){

            this.count = this.count+1; 
            this.counterChange.emit(this.count);
        }

        decrement(){
            this.count = this.count - 1; 
            this.counterChange.emit(this.count);
        }
    }
 ```

  - Step 5

Like any simple component, a component with two-way data binding can be used inside another component.
```
import {Component} from '@angular/core';

@Component({
    moduleId:module.id,
    selector:'my-app',
    template:`
  <div class="container">
     <br/>
    
     <countercomponent [(counter)]="c"></countercomponent>
     <br/>
     <h2>count = {{c}}</h2> 
     
  </div>
  `
})
export class AppComponent{

        c : number = 1; 
      
    }
```
The main thing you may want to notice the way value of a counter property is set inside AppComponent. Like ngModel directive, counter property is also set using the banana in box syntax [(counter)]

## Conclusion

Two-way data binding in Angular  is supported using the event and the property binding. There is no in-built two-way data binding. We can use the ngModel directive to use two-way data binding. Also, if required custom two-way data bindings can be created. Custom two-way data binding us useful in form controls.

In this post, we learned about ngModel and creating custom two-way data binding. I hope you find this post useful. Thanks for reading.

