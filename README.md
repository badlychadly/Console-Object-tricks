# Console-Object-tricks

Using the JavaScript Console object was great for debugging when I first started coding javascript, but when I found out about the debugger statement I did not have a huge need for it. Now that I have been coding JavaScript for a little while I find myself circling back and finding some cases where console is very useful. 

## CSS and Console.log
In case you didn't know you can actually style your `console.log` messages! I don't have a huge use for this but it's something I was not aware of and wanted to share it. To do this you need to add the parameter `%c` inside the string of your message, then in the next argument of `log()` add your css in a string. Here is an example `console.log("%c I'm blue!", "color: blue;")` will output your message in blue. You are not limited to just one style either. Lets change the font size `console.log("%c I'm blue!", "color: blue; font-size: 2rem;")`.

## Console.time()
One very useful method that can be used on the console object is `time()` with `timeEnd()`. With these methods we can track how long an operation takes. You can even pass a label to keep the timers oganized. 
```
console.time("100 times")
for (let i = 0; i <= 100; i++) {
	console.log(i)
}
console.timeEnd("100 times")

## output: 100 times: 26.44921875ms


console.time("1000 times")
for (let i = 0; i <= 1000; i++) {
	console.log(i)
}
console.timeEnd("1000 times")

##output: 1000 times: 227.530029296875ms
```
When you label them the output will display the label followed by the results. This is a great way to test you operations to get the fastest results.

## trace() and dir()
The last two methods I will go over is `trace()` and `dir()`. Using trace inside a nested function will output a stack trace of functions to give you insight on why and how your code ended up a certain way.
```
function myFunction() {
  myOtherFunction();
}

function myOtherFunction() {
  console.trace();
}

myFunction()
//outputs: 	myOtherFunction	@	VM1436:6
            myFunction	@	VM1436:2
            (anonymous)	@	VM1450:1
    
```

`dir` might be my favorite method so far. Mozilla docs describe it best 
```
The Console method dir() displays an interactive list of the properties of the specified JavaScript object. The output is presented as a hierarchical listing with disclosure triangles that let you see the contents of child objects.
In other words, console.dir() is the way to see all the properties of a specified JavaScript object in console by which the developer can easily get the properties of the object.
```
To get a small idea of this let's say we have an anonymous function inside another function that uses a variable declared in the parent scope.
```
let outerFunc = () => {
	let i = 1
	return () => {
		console.log(i)
    }
}
console.dir(outerFunc())

//output:  
anonymous()
  arguments: (...)
  caller: (...)
  length: 0
  name: ""
  __proto__: ƒ ()
  [[FunctionLocation]]: VM3962:3
  [[Scopes]]: Scopes[3]
    0: Closure (outerFunc) {i: 1}
    1: Script {first: ƒ, outerFunc: ƒ}
    2: Global {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, parent: Window, …}

```
You can see that whats returned is a listing of all of the properties of the anonymous child function, including the Closure and where the code was written! I've found `dir()` to be extremely useful when using JavaScript frameworks like react. I'm able to track down the code i'm curious about and get a better understanding of how it works.
Using tricks of the Console along with debugger will give you much more power over your code!


