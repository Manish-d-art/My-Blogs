# What is event delegation in JavaScript, why is it crucial ??๐ฅ๐

---

Let's go deep so there are no queries. So, Event delegation is a method for managing events effectively. Instead of adding an event listener to every similar element, we can add an event listener to a parent element and then use the .target(๐ง๐ต๐ฒ ๐๐ฎ๐ฟ๐ด๐ฒ๐ ๐ฒ๐๐ฒ๐ป๐ ๐ฝ๐ฟ๐ผ๐ฝ๐ฒ๐ฟ๐๐ ๐ฟ๐ฒ๐๐๐ฟ๐ป๐ ๐๐ต๐ฒ ๐ฒ๐น๐ฒ๐บ๐ฒ๐ป๐ ๐๐ต๐ฎ๐ ๐๐ฟ๐ถ๐ด๐ด๐ฒ๐ฟ๐ฒ๐ฑ ๐๐ต๐ฒ ๐ฒ๐๐ฒ๐ป๐) property of the event object to fire an event on a specific target and you'll understand why it is crucial at the end just stayย with me ๐.

### Before we get started, let us have a look at the event propagation: ๐ฉ๐๐๐๐๐๐ ๐๐๐ ๐ช๐๐๐๐๐๐๐๐๐

* Capturing phase: *the event goes down to the element.*
    
* Target phase: *the event reached the target element.*
    
* Bubbling Phase: *the event bubbles up from the element.*
    

![๐](https://cdn.hashnode.com/res/hashnode/image/upload/v1671903243578/9dcb36e0-e0ba-4901-a1b7-2544faa9671a.png align="center")

when a click happens on the link(*see fig 1.1*), then the DOM generates a click event right away. However, this event is not generated at the target element. Instead, the event is actually generated at the root of the document. So at the very top of the DOM tree.

And from there, the so-called **Capturing phase** happens, where the event then travels all the way down from the document route to the target element. And as the event travels down it will pass through every single parent element of the target element. So in our example, here is the HTML element, the body element, the section, then the paragraph, until it finally reaches its target.

As soon as it reaches the target, the target phase begins, where events can be handled right at the target. So, at the **target phase**, Event listeners wait for a certain event to happen on a certain element, and as soon as the event occurs it runs the attached callback function.

```javascript
document.querySelector('a').addEventListener('click', () => {
    alert('you clicked me');
});
```

In the above example, it will simply create this alert window.

All right, now, after reaching the target, the event then actually travels all the way up to the document route again, in the so-called **Bubbling Phase**. Just like the Capture phase, the event passes through all its parent elements and just the parents, so not through any sibling elements.

**One thing should be noted down**, the event can only be handled at the target and bubbling phase by default. However, we can set up event listeners in a way that they listen to events in the capturing phase instead.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671948229734/6a758bd1-d437-4e9a-859f-368d159b5fdd.jpeg align="center")

Also actually, not all types of events do have a Capturing and Bubbling instead.

All right, so I hope that all of this made sense about Bubbling and Capturing๐. Let's move forward...

### **How Does Event Delegation Work๐ค๐ค??**

```xml
<html>
    <head>
        <title> the DOM </title>
    </head>
<body>
    <div>
        <p>A simple page <a>click me</a> </p>
        <button>a simple button</button>
    </div>
</body>
</html>
```

With event delegation, you can handle the click event on the div rather than the button. Instead of the actual element(the *button*) that received the event, the concept is to **"delegate"** the handling of the event to a different element( *in this case, the div, which is a parent element*).

**view the JavaScript code below**๐...

```javascript
const div = document.getElementByTagName('div')[0]; 

div.addEventListener('click', (e) => {
    if(e.target.tagName === 'BUTTON') {
        console.log('button was click');
    }
});
```

The **target** property of the event object contains details about the actual receiving element of the event. We obtain the name of the element's tag from target.tagName and determine whether it is Button.

With this code, when you click the button, the event bubbles up to the div which handles the event.

### **Benefits of event delegation๐...**

* It's a useful pattern that allows you to write cleaner code and create fewer event Listeners with similar logic.
    
* Instead of attaching event listeners to individual elements, I will recommend you use event delegation for this purpose.
    

**Suppose**, if you wanted to hear click on every element with the .child class may be you'll do this.

```javascript
const children = document.querySelectorAll('.child');

children.forEach( child => 
    child.addEventListener('click', e => console.log('you clicked me'))
);
```

But with the event delegation, you would listen for all clicks on the document and ignore ones on elements without that .child class.

```javascript
document.addEventListener('click', e => {
    if(!e.target.matches('.child'))
        return;
    console.log(e.target);
}
```

<mark>Well, you must have thought of something.</mark>

*Isn't is bad for performance to listen to every click in the document.*

Surprisingly, it's actually better for performance to use this approach.

Okay, let me tell you why we don't attach eventListener to every element and that is because every event listner you create uses memory in the browser. And it's cheaper for the browser to track one event and fire it on every click that is to manage multiple events.

If youโre only listening for events on a single element, feel free to attach directly to that element. But if youโre listening for events on multiple elements, Iโd recommend using event delegation.

Congratulations on having in-depth understanding about event delegation if you have read this post attentively, in my opinion.

***"Never give up on your dreams because they do come true".***

If you have any questions, please let me know and I'll do my best to answer them.That's all I have today. folks, see you in my next blog๐โโ๏ธ...