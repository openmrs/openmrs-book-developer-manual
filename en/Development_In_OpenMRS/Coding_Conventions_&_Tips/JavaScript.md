<center><h1>JavaScript</h1></center>
**************************************

JavaScript will be a huge part of every project with the new format. Making sure you're caught up on the newest and greatest practices is a great way to start off your code looking nice with the side effect of high quality. With the newest releas of ECMAScript 6, and its large cross-browser support, there are a ton of new features to learn about, which you can find [here](http://es6-features.org). Now, lets get started!

## Const and Let

JavaScript now has a better form of scoped variables, and in two parts! The new keywords `const` and `let` are here to replace the usage of `var` for variable declarations. `const` variables are used to define variables that should not be redefined within their scope. For example,
```js
const numb = 0;
numb = 1 // Error: redefinition

const mySet = Set();
mySet.add(0); // No Error
```
As you can see, you cannot set a `const` variable to any other value, however, you can still modify the value if it is an object, as shown by the `Set` object above. An odd exceptions is that `const` can be used in loops over objects like such:
```js
const list = [2, 3, 5, 4];
for(const elem of list){
	console.log(elem);
}
// Output: 2 3 5 4
```
The above code will act like a for loop with a hidden loop index variable, and then will declare a `const` variable with the name of `elem` at each iteration.

Unlike a `const` variable, `let` may be modified just like a variable defined with `var`. This type of delaration is most often used in loops such as:
```js
const list = [4, 5, 3, 7];
for(let i = 0; i < list.length; i++){
	 console.log(list[i]);
}
// Output: 4 5 3 7

const queue = [3, 4, 9, 8]
let next = undefined;
while(queue.length > 0){
	 next = queue.unshift();
	 console.log(next);
}
// Output: 3 4 9 8
```
Unlike `var`, both `const` and `var` are limited to the scopes they are defined in, not the scope of the function as a whole. Now, variables defined in loops stay in loops!

## Promises

Promises are a new way that JavaScript looks to solve its long-standing problem of asynchronous functions and callbacks. Make sure you read the section on `async` and `await` before writing any code with promises as using those two keywords can make your code look even better!

### General Use

JavaScript has always been a huge pain when dealing with asynchronous functions. Because JavaScript is executed on only 1 thread, and IO operations, such as getting the contents of a file, or posting to the server, required the use of callbacks, as demonstrated below:
```js
/* Async function to get the content from an html file */
function loadFile(file, callback){
	 var content = // get file content
	 if(/* An Error occured, like content came back emtpy */){
		  throw new Error("Error Message");
	 } else {
		  callback(content);
	 }
}

/* Insert the html given at the end of the element with the given id */
function insertHTML(id, html){
	 document.getElementById(id).insertAdjacentHTML('afterend', html);
}

function example(){
	 /* Get the HTML content from test.html */
	 loadFile("test.html", function(content){
		  /* Insert the html as the child of the element with id = mycontent */
		  insertHTML("mycontent", content);
	 });

	 /* Insert the HTML, CSS, and JavaScript for a fragment */
	 loadFile("fragment.css", function(cssFile){
		  insertHTML("myfragment", "<style>" + cssFile + "</style>");
		  loadFile("fragment.html", function(htmlFile){
			   insertHTML("myfragment", htmlFile);
			   loadFile("fragment.js", function(jsFile){
				    insertHTML("myfragment", "<script>" + jsFile + "</script>");
			   });
		  });
	 });
}

example();
```
The above code would insert the html from the document into an element, but could only do it for one document. While it doesn't look so bad at the beginning, loading content from multiple files at the same time _and_ waiting for the data retrieval to finish required a callback for each file and the code looked extremely ugly and was difficult to read. JS6 provides a new way to use asynchrouns functions through the use of `Promise`s. The same code above can be written using promises as follows:
```js
/* Async function to get the content from an html file */
function loadFile(file){
	 return new Promise((resolve, reject) => {
		  const content = // get file content
		  if(/* An Error occured, like content came back emtpy */){
			   reject(new Error("Error Message"));
		  } else {
			   resolve(content);
		  }
	 });
}

/* Insert the html given at the end of the element with the given id */
function insertHTML(id, html){
	 document.getElementById(id).insertAdjacentHTML('afterend', html);
}

function example(){
	 /* Get the HTML content from test.html */
	 loadFile("test.html").then((content) => {
	 	/* Insert the html as the child of the element with id = mycontent */
	 	insertHTML("mycontent", content);
	 });

 /* Insert the HTML, CSS, and JavaScript for a fragment */
	 loadFile("fragment.css").then((cssFile) => {
		  insertHTML("myfragment", "<style>" + cssFile + "</style>");
		  loadFile("fragment.html");
	 }).then((htmlFile) => {
		  insertHTML("myfragment", htmlFile);
		  loadFile("fragment.js");
	 }).then((jsFile) => {
		  insertHTML("myfragment", "<script>" + jsFile + "</script>");
	 });
}

example();
```
As you can see, while the actual length of the code does not improve, the readablity does. It should now be clear that each part is meant to happen after the previous part is finished. Additionally, the tabbing with the callbacks does not go to infinity but stays at between 0 and 1 tabs.

### JQuery

With the new promises, it's always helpful to understand how they work with some of the large libraries out there, like JQuery.

The good thing is, if you are using JQuery 3.0+, its `ajax` functions already return the new JavaScript Promises! If you are using JQuery previous to 3.0, then you can simply wrap the `ajax` function in a JS6 Promise. You can see each below:
```js

const options = /* Your Ajax options */

/* JQuery 3.0+ */
$.ajax(options).then((response) => {
	 /* Do whatever with response */
});

/* Before JQuery 3.0 */
function myAjax(options){
	 return new Promise((resolve, reject) {
		  $.ajax(options).done(resolve).fail(reject);
	 });
}

myAjax(options).then((response) => {
 /* Do whatever with response */
});
```
The one thing you'll have to be aware of is ensuring that you have the appropriate parameters in your response function (in then).

### async and await

Along with promises, there are two new keywords that help make code that uses promises look and operate much more cleanly.

The `async` keyword is used just before the function name (after `static` if in a class). This keyword makes the function implicitly return a promise, so you no longer need to wrap the inside of the function in a promise! What ever you return from the function is what would have been a parameter in the Promise `resolve` function from above. The Error thrown below would be equivalent to calling the `reject` function as above.

The `await` function will suspend the code where it is, in a way that is non-blocking, and wait for the promise that comes directly after it to complete. Once the Promise has been completed, it will resume the function right where it left off. **Note: This keyword can only be used in a an `async` function.**

The impact of these keywords is _huge_ and can easily make your code far cleaner. Take the previous Promise example for getting files. Using `await` and `async` makes it look like this:
```js
/* Async function to get the content from an html file */
async function loadFile(file){
	 const content = // get file content
	 if(/* An Error occured, like content came back emtpy */){
		  throw new Error(`Error: Could not retrieve the contents of file ${file}`);
	 }
	 return content;
}

/* Insert the html given at the end of the element with the given id */
function insertHTML(id, html){
	 document.getElementById(id).insertAdjacentHTML('afterend', html);
}

async function example(){
	try {
		/* Get the HTML content from test.html */
		const content = await loadFile("test.html");
		/* Insert the html as the child of the element with id = mycontent */
		insertHTML("mycontent", content);

		/* Insert the HTML, CSS, and JavaScript for a fragment */
		const cssFile = await loadFile("fragment.css");
		insertHTML("myfragment", "<style>" + cssFile + "</style>");
		const htmlFile = await loadFile("fragment.html");
		insertHTML("myfragment", htmlFile);
		const jsFile = await loadFile("fragment.js");
		insertHTML("myfragment", "<script>" + jsFile + "</script>");
	} catch (err) {
		/* Handel error thrown by insertHTML */
	}
}

example();
```
**Note: The try/catch block is not necessary, but used for demonstration purposes.**

You'll notice that this is _far_ cleaner than both the callback and Promise way to write JavaScript. It retains the readabilty of the Promise, and improves upon the organization and look of the code. Even more, try/catch blocks can finally be used and it still looks nice! These two keywords will make your life far easier.
