# Learning Flex Box
```ts
<section id="container">
    <div id="child1" class="child"></div>
    <div id="child2" class="child"></div>
    <div id="child3" class="child"></div>
</section>
```

```css
#container {
    display: flex;
    width: 100%;
    height: 700px;
    border: 1px solid black;
    flex-direction: row; 
    justify-content: flex-start; /*Main axis*/
    align-items: center; /*Cross aixs*/
}

.child {
    width: 200px;
    height: 200px;
    /* flex: 1;*/
} 

#child1 {
    background-color: red;
    /* flex: 2; */
}

#child2 {
    background-color: green;
}

#child3 {
    background-color: blue;
}
```
