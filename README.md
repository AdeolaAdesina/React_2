# Advanced JSX

## class vs className 

This lesson will cover more advanced JSX. You’ll learn some powerful tricks and some common errors to avoid.

Grammar in JSX is mostly the same as in HTML, but there are subtle differences to watch out for. The most frequent of these involves the word class.

In HTML, it’s common to use class as an attribute name:

```
<h1 class="big">Title</h1>
```

In JSX, you can’t use the word class! You have to use className instead:

```
<h1 className="big">Title</h1>
```

This is because JSX gets translated into JavaScript, and class is a reserved word in JavaScript.

When JSX is rendered, JSX className attributes are automatically rendered as class attributes.


## Self-Closing Tags

Another common JSX error involves self-closing tags.

What’s a self-closing tag?

Most HTML elements use two tags: an opening tag ```(<div>)```, and a closing tag ```(</div>)```. However, some HTML elements such as ```<img>``` and ```<input>``` use only one tag. The tag that belongs to a single-tag element isn’t an opening tag or a closing tag; it’s a self-closing tag.

When you write a self-closing tag in HTML, it is optional to include a forward slash immediately before the final angle bracket:

```
// Fine in HTML with a slash:
<br />

// Also fine, without the slash:
<br>
```
But, in JSX, you have to include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error:

```
// Fine in JSX:
<br />

// NOT FINE AT ALL in JSX:
<br>
```


Example:

```
const profile = (
  <div>
    <h1>John Smith</h1>
    <img src="images/john.png"/>
    <article>
      My name is John Smith.
      <br />
      I am a software developer.
      <br />
      I specialize in creating React applications.
    </article>
  </div>
);
```


## JavaScript In Your JSX In Your JavaScript

So far, we’ve focused on writing JSX expressions. It’s similar to writing bits of HTML, but inside of a JavaScript file.

In this lesson, we’re going to add something new: regular JavaScript, written inside of a JSX expression, written inside of a JavaScript file.

Instructions


Starting on line 7, carefully write the following code.

root.render(<h1>2 + 3</h1>);

What do you think will appear in the browser?


![Screenshot 2023-11-14 at 14 34 49](https://github.com/AdeolaAdesina/React_2/assets/29931071/32260328-db4c-4c86-b542-d763d22ecae0)



## Curly Braces in JSX

The code in the last exercise didn’t behave as one might expect. Instead of adding 2 and 3, it printed out “2 + 3” as a string of text. Why?

This happened because 2 + 3 is located in between ```<h1>``` and ```</h1>``` tags.

Any code in between the tags of a JSX element will be read as JSX, not as regular JavaScript! JSX doesn’t add numbers—it reads them as text, just like HTML.

You need a way to write code that says, “Even though I am located in between JSX tags, treat me like ordinary JavaScript and not like JSX.”

You can do this by wrapping your code in curly braces.


1.
Add a pair of curly braces to the code from the last exercise so that your JSX expression looks like this:

```
<h1>{2 + 3}</h1>
```

Everything inside of the curly braces will be treated as regular JavaScript.


![Screenshot 2023-11-14 at 14 36 27](https://github.com/AdeolaAdesina/React_2/assets/29931071/9455901c-2006-481d-bb48-d3964cfce456)




# Variables in JSX

When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.

That means that you can access variables while inside of a JSX expression, even if those variables were declared outside of the JSX code block.

```
// Declare a variable:
const name = 'Gerdo';

// Access your variable inside of a JSX expression:
const greeting = <p>Hello, {name}!</p>;
```

Instructions

1.
Replace root.render()‘s argument with a JSX <h1></h1>.

Using curly braces, set the <h1></h1> tag’s inner text equal to theBestString.


![Screenshot 2023-11-14 at 14 39 11](https://github.com/AdeolaAdesina/React_2/assets/29931071/841ce2f0-37a3-4eab-b953-1a923a4251b5)



## Variable Attributes in JSX

When writing JSX, it’s common to use variables to set attributes.

Here’s an example of how that might work:

```
// Use a variable to set the `height` and `width` attributes:

const sideLength = "200px";

const panda = (
  <img 
    src="images/panda.jpg" 
    alt="panda" 
    height={sideLength} 
    width={sideLength} />
);
```

Notice how in this example, the ```<img />‘s``` attributes each get their own line. This can make your code more readable if you have a lot of attributes for one element.

Object properties are also often used to set attributes:

```
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
}; 

const panda = (
  <img 
    src={pics.panda} 
    alt="Lazy Panda" />
);

const owl = (
  <img 
    src={pics.owl} 
    alt="Unimpressed Owl" />
);

const owlCat = (
  <img 
    src={pics.owlCat} 
    alt="Ghastly Abomination" />
);
```


Example:

![Screenshot 2023-11-14 at 14 42 11](https://github.com/AdeolaAdesina/React_2/assets/29931071/68974c74-3794-42c9-ad6f-61bb9fb15a0f)



## Event Listeners in JSX

JSX elements can have event listeners, just like HTML elements can. Programming in React means constantly working with event listeners.

You create an event listener by giving a JSX element a special attribute. Here’s an example:

```
<img onClick={clickAlert} />
```

An event listener attribute’s name should be something like onClick or onMouseOver: the word on plus the type of event that you’re listening for. Look through the common components list in React docs to browse supported event names.

An event listener attribute’s value should be a function. The above example would only work if clickAlert were a valid function that had been defined elsewhere:

```
function clickAlert() {
  alert('You clicked this image!');
}

<img onClick={clickAlert} />
```

Note that in HTML, event listener names are written in all lowercase, such as onclick or onmouseover. In JSX, event listener names are written in camelCase, such as onClick or onMouseOver.


Example:

1.

Take a look at line 19. root.render() is being passed a null argument.

Render kitty by replacing the null with kitty.



2.

Add an onClick attribute to the ```<img />``` element. Set onClick‘s value equal to the makeDoggy function.

Remember, since attributes are a part of JSX expressions, you will need to inject JavaScript in order to use makeDoggy.

Click Run, and then click on the browser image to change the kitty into a doggy.


```
import React from 'react';
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
function makeDoggy(e) {
  // Call this extremely useful function on an <img>.
  // The <img> will become a picture of a doggy.
  e.target.setAttribute('src', 'https://content.codecademy.com/courses/React/react_photo-puppy.jpeg');
  e.target.setAttribute('alt', 'doggy');
}

const kitty = (
	<img 
		src="https://content.codecademy.com/courses/React/react_photo-kitty.jpg" 
		alt="kitty" onClick={makeDoggy} />
);

root.render(kitty);
```

![Screenshot 2023-11-14 at 14 59 22](https://github.com/AdeolaAdesina/React_2/assets/29931071/c5ffe882-37ed-4850-af4b-fbce78f73ccf)



## JSX Conditionals: If Statements That Don't Work

Great work! You’ve learned how to use curly braces to inject JavaScript into a JSX expression!

Here’s a rule that you need to know: you can not inject an if statement into a JSX expression.

This code will break:

```
(
  <h1>
    {
      if (purchase.complete) {
        'Thank you for placing an order!'
      }
    }
  </h1>
)
```

What if you want a JSX expression to render but only under certain circumstances? You can’t inject an if statement. What can you do?

You have lots of options. In the next few lessons, we’ll explore some simple ways to write conditionals (expressions that are only executed under certain conditions) in JSX.


## JSX Conditionals: If Statements That Do Work

How can you write a conditional if you can’t inject an if statement into JSX?

One option is to write an if statement and not inject it into JSX.

Look at if.js. Follow the if statement, all the way from line 8 down to line 20.

if.js works because the words if and else are not injected in between JSX tags. The if statement is on the outside, and no JavaScript injection is necessary.

This is a common way to express conditionals in JSX.


Example:

```
import React from 'react';
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
let message;

if (user.age >= drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  );
}

root.render(message);
```


Instructions

Open app.js.

Starting on line 18, write an if/else statement, using if.js as a guide.

If coinToss() is equal to 'heads', execute img = ```<img src={pics.kitty} />```.

Inside of the else clause, execute img = ```<img src={pics.doggy} />```.

In other words, if the coin lands heads, then you should get a picture of a kitty, and if the coin lands tails, then you should get a picture of a doggy.


2.
At the bottom of the file, call root.render().

For root.render()‘s argument, pass in img.

Click Run. Refresh the browser several times. Does the picture change?


```
import React from 'react';
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
function coinToss() {
  // This function will randomly return either 'heads' or 'tails'.
  return Math.random() < 0.5 ? 'heads' : 'tails';
}

const pics = {
  kitty: 'https://content.codecademy.com/courses/React/react_photo-kitty.jpg',
  doggy: 'https://content.codecademy.com/courses/React/react_photo-puppy.jpeg'
};
let img;

// if/else statement begins here:
if (coinToss() ==='heads') {
  img = 
    <img src={pics.kitty} />
  ;
} else {
  img = 
    <img src={pics.doggy} />
  ;
}

root.render(img)
```


## JSX Conditionals: The Ternary Operator

There’s a more compact way to write conditionals in JSX: the ternary operator.

The ternary operator works the same way in React as it does in regular JavaScript. However, it shows up in React surprisingly often.

Recall how it works: you write x ? y : z, where x, y, and z are all JavaScript expressions. When your code is executed, x is evaluated as either “truthy” or “falsy”. If x is truthy, then the entire ternary operator returns y. If x is falsy, then the entire ternary operator returns z.

Here’s how you might use the ternary operator in a JSX expression:

```
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```

In the above example, if age is greater than or equal to drinkingAge, then headline will equal <h1>Buy Drink</h1>. Otherwise, headline will equal ```<h1>```Do Teen Stuff```</h1>```.


## JSX Conditionals: &&

We’re going to cover one final way of writing conditionals in React: the && operator.

Like the ternary operator, && is not React-specific, but it shows up in React very often.

In the last two exercises, you wrote statements that would sometimes render a kitty and other times render a doggy. && would not have been the best choice for that code.

&& works best for conditionals that will sometimes do an action but other times do nothing at all.

Here’s an example:

```
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

If the expression on the left of the && evaluates as true, then the JSX on the right of the && will be rendered. If the first expression is false, however, then the JSX to the right of the && will be ignored and not rendered.


## .map in JSX

The .map() array method comes up often in React. It’s good to get in the habit of using it alongside JSX.

If you want to create a list of JSX elements, then using .map() is often the most efficient way. It can look odd at first:

```
const strings = ['Home', 'Shop', 'About Me'];

const listItems = strings.map(string => <li>{string}</li>);

<ul>{listItems}</ul>
```

In the above example, we start out with an array of strings. We call .map() on this array of strings, and the .map() call returns a new array of ```<li>s```.

On the last line of the example, note that {listItems} will evaluate to an array, because it’s the returned value of .map()! JSX ```<li>s``` don’t have to be in an array like this, but they can be.

```
// This is fine in JSX, not in an explicit array:
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>

// This is also fine!
const liArray = [
  <li>item 1</li>, 
  <li>item 2</li>, 
  <li>item 3</li>
];

<ul>{liArray}</ul>
```

Example:

```
import React from 'react';
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
const people = ['Rowe', 'Prevost', 'Gare'];

const peopleList = people.map(person =>
  // expression goes here:
  <li>{person}</li>
);

// root.render goes here:
root.render(<ul>{peopleList}</ul>);
```

![Screenshot 2023-11-14 at 15 22 47](https://github.com/AdeolaAdesina/React_2/assets/29931071/27e35254-95f3-4fd9-9024-d5f58eaf5653)



## Keys

When you make a list in JSX, sometimes your list will need to include something called keys:

```
<ul>
  <li key="li-01">Example1</li>
  <li key="li-02">Example2</li>
  <li key="li-03">Example3</li>
</ul>
```

A key is a JSX attribute. The attribute’s name is key. The attribute’s value should be something unique, similar to an id attribute.

keys don’t do anything visible! React uses them internally to keep track of lists. If you don’t use keys when you’re supposed to, React might accidentally scramble your list items into the wrong order.

Not all lists need to have keys. A list needs keys if either of the following is true:

The list items have memory from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off. The items shouldn’t get amnesia when they render.

A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.
If neither of these conditions is true, then you don’t have to worry about keys. If you aren’t sure, then it never hurts to use them!


Example:

```
import React from 'react';
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
const people = ['Rowe', 'Prevost', 'Gare'];

const peopleList = people.map((person,i) =>
  // expression goes here:
  <li key={'person_'+ i}>{person}</li>
);

// root.render goes here:
root.render(peopeList);
```


## React.createElement

You can write React code without using JSX at all!

The majority of React programmers do use JSX, but you should understand that it is possible to write React code without it.

The following JSX expression:

```
const h1 = <h1>Hello world</h1>;
```

can be rewritten without JSX, like this:

```
const h1 = React.createElement(
  "h1",
  null,
  "Hello world"
);
```

When a JSX element is compiled, the compiler transforms the JSX element into the method that you see above: React.createElement(). Every JSX element is secretly a call to React.createElement().



