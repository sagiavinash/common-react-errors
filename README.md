#common reactjs errors

1.Uncaught TypeError: Cannot read property '_currentElement' of null
```
missing element source import/require.
```

2.UncaughtError: Cannot find module <module_path>
```
Webpack parse error in that module. check webpack dev server logs for source of error.
```
3.maximum callstack exceeded
```
setState in componentDidUpdate instead of componentWillReceiveProps
```
4.Uncaught Error: Invariant Violation: processUpdates(): Unable to find child 4 of element.
```
This probably means the DOM was unexpectedly mutated (e.g., by the browser), usually due to forgetting a <tbody> when using tables, nesting tags like <form>, <p>, or <a>, or using non-SVG elements in an <svg> parent. Try inspecting the child nodes of the element with React ID .0.1.0.0.0.1.0.$reachedout.1
```
5.Unhandled promise rejection TypeError: Cannot read property 'length' of undefined

6.Uncaught TypeError: this._callbacks[id] is not a function
```
https://github.com/facebook/flux/issues/273
http://stackoverflow.com/questions/32225534/reactjs-flux-dispatcher-js-error-this-callbacksid-is-not-a-function
In classes syntax methods used to evaluate state should be above the “state =” initialization of state as babel compiled code is series of property assignments to "this” and the order of assignment matters for accessing a property
```
