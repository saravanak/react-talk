class: center, middle

# React Basics 
   *by*   

      Old Weaver
---

#Who Am I?

Saravana Kumar  @ saro

--
 - I belong to Ajira.tech

--
 - Late entrant to Web Tech
--

 - Love Vim 

---

## Clauses


I am no authority in React. Take my comments during this session with a pinch of
salt.

--

So , if you already know about React and are planning to bash me with
advanced stuff *only you know about*, please

--

shut up

--

#shout up
As we are here to learn about stuff.

--

I will try to explain the basics of React. This is to cover the greatest common
denomintator's aspirations. 


--

- Advanced concepts are NOT covered
- Tooling is NOT covered but is important!

--

..but if you think about it deeply, thats all there is in React!

---
## Outcome

you should go back with good memories of the talk 

--

and be empowered to try out some stuff in react.

---
# Javascript - Recap 

## Simple DOM creation using javascript

--

```javascript
var img = document.createElement('IMG');
img.setAttribute('src', 'delete.gif');
img.onclick = function(){
  removeContact(tr);
}
td1.appendChild(img);
```
---


# Introduction

 React is just a function:

  <blockquote>
    React components implement a render() method that takes input data and
    returns what to display.
  </blockquote>

--

  ```
  f(model) = view
  ```

--

  **Examples**


  ```javascript
  render([post[comments]]) = blog
  render([cat_data]) = cat profile page
  ```
--

  ```javascript
  render([post]) = blog edit page
  render([cat_data]) = cat profile edit page
  ```

---

# So, what is a model?

  ```
  f(model) = view
  ```
--

  ```javascript
  render([post[comments]]) = blog //static
  render([cat_data]) = cat profile page //static
  ```

--

  ```javascript
  render([post]) = blog edit page //dynamic
  render([cat_data]) = cat profile edit page //dynamic
  ```

--

  Static data
    - Configuration options
    - Color values, etc
    - Read only data
--
  Dynamic data
    - Duh, things that can change while the user is *interacting*
    - Edit comment and post it
    - Animations
    - Form validation semantics


---

## Question

  Can you identify the model here?

--

  ```javascript
  var img = document.createElement('IMG');
  img.setAttribute('src', 'delete.gif');
  img.onclick = function(){
    removeContact(tr);
  }
  td1.appendChild(img);
  ```
--
  **Is this static or dynamic?**
---

# What else is React?
[ From the Horses' mouth ]( https://facebook.github.io/react/ )

**JUST THE UI**

--

Lots of people use React as the V in MVC. Since React makes no assumptions about
the rest of your technology stack, it's easy to try it out on a small feature in
an existing project.

--

**VIRTUAL DOM**

--

React abstracts away the DOM from you, giving a simpler programming model and
better performance. React can also render on the server using Node, and it can
power native apps using React Native.

--

**DATA FLOW**

--

React implements one-way reactive data flow which reduces boilerplate and is
easier to reason about than traditional data binding.

---

## Show me some examples

--

[Basic Props](/react-properties/defining-properties-jsx.html)

--

  ```javascript
  render : function() {
    return <div>hello {this.props.name}!</div>;
  }
    ```

--

React abstracts away the DOM from you, giving a simpler programming model and ..

--

* **Are you kidding ???**

---

## Virtual DOM 

http://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/

--

So, whenever we want to dynamicly change the content of the web page, we modify
the DOM:

--

```javascript
var item = document.getElementById("myLI");
item.parentNode.removeChild(item);
```

--

**Problems**

--

The HTML DOM is always tree-structured, because of which:

--

 - It’s hard to manage. Imagine that you have to tweak an event handler. If you
lost the context, you have to dive really deep into the code to even know what’s
going on. Both time-consuming and bug-risky.

--

 - It’s inefficient. Do we really need to do all this findings manually? Maybe we
can be smarter and tell in advance which nodes are to-be-updated?

---

## Virtual DOM  -- how react helps

http://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/

- The Virtual DOM is an abstraction of the HTML DOM.

--

- it’s better to think of the virtual DOM as React’s local and simplified copy
of the HTML DOM

--

It allows React to do its computations within this abstract world and skip the
“real” DOM operations, often slow and browser-specific.

--

<blockquote>
Changes are first made to the virtual DOM when data is changed. These changes
are then diffed with the actual DOM, and only changing components are
re-rendered. This approach leads to a “one-way reactive data flow which reduces
boilerplate and is easier to reason about than traditional data binding.”

</blockquote>
[source](http://webtech-cs294.tumblr.com/post/110530653639/react-a-simple-approach-to-reactive-programming)

---

## Question

  Can you identify the bindings here?

--

  ```javascript
  var img = document.createElement('IMG');
  img.setAttribute('src', 'delete.gif');
  img.onclick = function(){
    removeContact(tr);
  }
  td1.appendChild(img);
  ```
--
  **Is this oneway or twoway?**

---
## Simple 2 way binding in javscript

 - Uses pubsub model, using the jquery $({}) object.
  [Example](./Easy 2 way binding.pdf)

---
# advtantages of two way binding

--

This is a very solid concept to build a web application on top of, because it
makes the "Model" abstraction a safe, atomic data source to use everywhere
within the application. Say, if a model, bound to a view, changes, then its
matching piece of UI (the view) will reflect that, no matter what. And the
matching piece of UI (the view) can safely be used as a mean of collecting user
inputs/data, so as to maintain the application data up-to-date.[1]

[1] - http://stackoverflow.com/questions/13504906/what-is-two-way-binding

---
# problems of two way bindings

--

with large scale

They're bad because it makes it too hard to reason about. With one way data flow
(and especially using something like Redux and Immutable.js), you know much more
clearly what's happening in your application. Also check out Christian Alfoni's
Cerebral for further evolution of this[1]

[1] - https://www.reddit.com/r/reactjs/comments/3mn9cf/why_is_localized_state_and_twoway_binding_a_bad/

---
---

## Revision time

http://blog.reverberate.org/2014/02/react-demystified.html

---

[Balmer
Peak](./react-properties/react-0.8.0/examples/ballmer-peak/)

--

```javascript
var BallmerPeakCalculator = React.createClass({
  getInitialState: function() {
    return {bac: 0};
  },
  handleChange: function(event) {
    this.setState({bac: event.target.value});
  },
  render: function() {
    var bac;
    var pct;
    pct = computeBallmerPeak(this.state.bac);
    ....
    return (
      <div>
      ...
        <p>
          If your BAC is{' '}
          <input type="text" 
            onChange={this.handleChange} 
            value={this.state.bac} />
          {', '}then <b>{pct}</b> of your lines 
              of code will have bugs.
        </p>
      </div>
    );
  }
});
```

---
class: center, middle
background-image: url(./immutable_state.png)
http://stackoverflow.com/questions/28032173/reactjs-whats-the-real-world-use-of-immutability-helpers-in-react
---
## Animation

[Again a state
example](/react-properties/react-0.8.0/examples/transitions)

  ```javascript
  tick: function() {
    this.setState({start: this.state.start + 1});
  },

  render: function() {
          var children = [];
          var pos = 0;
          var colors = ['red', 'gray', 'blue'];
          for (var i = this.state.start; 
                  i < this.state.start + 3; i++) {
            var style = {
left: pos * 128,
      background: colors[i % 3]
            };
            pos++;
            children.push(<div key={i} 
                    className="animateItem" style={style}>{i}
                    </div>);
          }
        }
```
---
## states and props : differences

State has data that you own. Props has data that you borrow.

--

You can change your own data. 

--

you have to ask someone else to change your props.


Testing react views : show our snippet.
---
##One way binding

Dependency tracking is complex.
Finding side effects in two way bound code is nightmarish.
--

See 00:40:00 of the video

--

One way binding == state machine pattern, you know what exactly happens in your
app. Flux is an enabler here.

--

 [http://staal.io/blog/2014/02/05/2-way-data-binding-under-the-microscope/]

---

## Other examples in the ppt

[example](./react-properties/react-0.8.0/examples/)
[memorygame](./slingshot/dist/)
[source for memory game](https://github.com/saravanak/slingmemory)

---

## states and props : differences

State has data that you own. Props has data that you borrow.

--

You can change your own data. 

--

you have to ask someone else to change your props.


Testing react views : show our snippet.
---
##One way binding

Dependency tracking is complex.
Finding side effects in two way bound code is nightmarish.
--

See 00:40:00 of the video

--

One way binding == state machine pattern, you know what exactly happens in your
app. Flux is an enabler here.

--

 [http://staal.io/blog/2014/02/05/2-way-data-binding-under-the-microscope/]

---

## In the wild

https://github.com/fedosejev/shopping-list-react/

---
## Resources

https://facebook.github.io/react/docs/getting-started.html

--

Thinking in React:
https://facebook.github.io/react/docs/thinking-in-react.html

--

Simple examples in react

http://react.rocks

--


Props vs State deep dive:
https://github.com/uberVU/react-guide/blob/master/props-vs-state.md

--

Dont miss this one if you need to know the internals:

http://jlongster.com/Removing-User-Interface-Complexity,-or-Why-React-is-Awesome

---

General web stuff

--

[https://frontendmasters.gitbooks.io/]

--

[https://remysharp.com/2015/10/14/the-art-of-debugging]

---

## Credits

This presentation is made by simple but awesome [Remark](https://github.com/gnab/remark/)

---
class: center, middle

background-image: url(nandri.jpg)


