# Common errors faced when using React & probable causes

1. **Uncaught TypeError: Cannot read property '_currentElement' of null**
- missing element source import/require.

2. **UncaughtError: Cannot find module <module_path>**
- Webpack parse error in that module. check webpack dev server logs for source of error.

3. **maximum callstack exceeded**
- setState in componentDidUpdate instead of componentWillReceiveProps.

4. **Uncaught Error: Invariant Violation: processUpdates(): Unable to find child 4 of element. This probably means the DOM was unexpectedly mutated (e.g., by the browser), usually due to forgetting a &lt;tbody&gt; when using tables, nesting tags like &lt;form&gt;, &lt;p&gt;, or &lt;a&gt;, or using non-SVG elements in an &lt;svg&gt; parent. Try inspecting the child nodes of the element with React ID .0.1.0.0.0.1.0.1**
- this error occurs when user tries to interact with the app after a react error has already occurred and corrupted the component tree.

5. **Uncaught TypeError: this._callbacks[id] is not a function**
- https://github.com/facebook/flux/issues/273
- http://stackoverflow.com/questions/32225534/reactjs-flux-dispatcher-js-error-this-callbacksid-is-not-a-function

6. **In classes syntax methods used to evaluate state should be above the “state =” initialization of state as babel compiled code is series of property assignments to "this” and the order of assignment matters for accessing a property**

7. **Uncaught TypeError: type.toUpperCase is not a function**
- when component definition is undefined.

8. **this.someMethod doesnt exist**
- when someMethod is defined using ES7 static method syntax (usually for autobinding this) and this method is declared below the method in which the call is then it leads to a ReferenceError because babel transpiles ES6 class methods to this.method = statements; and declarations below the statements are not available.
ES6 arrow functions -> babel transpiles them to a ES5 code that doesnt allow binding both this, arguments. so work around is to put a closure of IIFE arrow function to capture this and return a simple function so that bind works as it should.

9. **Cannot read property 'context' of null**
- maybe due to forceUpdate() calls.
https://github.com/facebook/react/issues/3585

10. **Infinite loop:**
- As of jan, 2016, Debugging infinite loops is better in firefox as it shows a modal with a button “debug script” which allows us to move to the detected start of the loop.
- Its generally caused by setState -> render -> componentDidUpdate -> setState loops. so a faulty purerender condition might be the reason.

11. **refs are undefined or setState invalid after unmount**
- things running setTimeout are not guarenteed to be running before component is unmounted so use _isMounted flag to check before executing. IsMounted is an antipattern use instance properties instead. https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html.

12. **warning.js:45 Warning: This synthetic event is reused for performance reasons. If you're seeing this, you're calling `stopPropagation` on a released/nullified synthetic event. This is a no-op. See https://fb.me/react-event-pooling for more information.warning @ warning.js:45stopPropagation @ SyntheticEvent.js:111loadNext**
- trying to run e.stopPropagation() in an async runtime. use e.persist() beore & outside the async runtime.

13. **TypeError: Cannot read property 'destroy' of undefined**
- if this is not referring to the component instance, common occurence is using this.props inside a stateless function component definition.

14. **SimpleEventPlugin.js:580 Uncaught (in promise) TypeError: Cannot read property 'remove' of undefined**
- Error in Component Render function (list items).
- "if an error occurs in unmount of a child component then parent component unmount will go infinite loop”.

