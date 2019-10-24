<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [Setup][1]
    -   [createInjectorsEnhancer][2]
        -   [Parameters][3]
        -   [Examples][4]
-   [Injectors][5]
    -   [injectReducer][6]
        -   [Parameters][7]
        -   [Examples][8]
    -   [useInjectReducer][9]
        -   [Parameters][10]
        -   [Examples][11]
    -   [injectSaga][12]
        -   [Parameters][13]
        -   [Examples][14]
    -   [useInjectSaga][15]
        -   [Parameters][16]
        -   [Examples][17]
-   [Misc][18]
    -   [forceReducerReload][19]
        -   [Parameters][20]
        -   [Examples][21]
    -   [SagaInjectionModes][22]
        -   [Properties][23]

## Setup




### createInjectorsEnhancer

Creates a store enhancer that when applied will setup the store to allow the
injectors to work properly

#### Parameters

-   `params` **[Object][24]** 
    -   `params.runSaga` **[function][25]** A function that runs a saga. Should usually be `sagaMiddleware.run`
    -   `params.createReducer` **[function][25]** A function that should create and
        return the root reducer. It's passed the injected reducers as the first
        parameter. These should be added to the root reducer using `combineReducer`
        or a similar method.

#### Examples

```javascript
import { createStore } from "redux"
import { createInjectorsEnhancer } from "redux-injectors"

function createReducer(injectedReducers = {}) {
 const rootReducer = combineReducers({
   ...injectedReducers,
   // other non-injected reducers can go here...
 });

 return rootReducer
}
const runSaga = sagaMiddleware.run

const store = createStore(
  createReducer(),
  initialState,
  createInjectorsEnhancer({
    createReducer,
    runSaga,
  })
)
```

## Injectors




### injectReducer

A higher-order component that dynamically injects a reducer when the
component is instantiated

#### Parameters

-   `params` **[Object][24]** 
    -   `params.key` **[string][26]** The key to inject the reducer under
    -   `params.reducer` **[function][25]** The reducer that will be injected

#### Examples

```javascript
class BooksManager extends React.PureComponent {
  render() {
    return null;
  }
}

export default injectReducer({ key: "books", reducer: booksReducer })(BooksManager)
```

### useInjectReducer

A react hook that dynamically injects a reducer when the hook is run

#### Parameters

-   `params` **[Object][24]** 
    -   `params.key` **[string][26]** The key to inject the reducer under
    -   `params.reducer` **[function][25]** The reducer that will be injected

#### Examples

```javascript
function BooksManager() {
  useInjectReducer({ key: "books", reducer: booksReducer })

  return null;
}
```

### injectSaga

A higher-order component that dynamically injects a saga when the component
is instantiated. There are several possible "modes" / "behaviours" that
dictate how and when the saga should be injected and ejected

#### Parameters

-   `params` **[Object][24]** 
    -   `params.key` **[string][26]** The key to inject the saga under
    -   `params.saga` **[function][25]** The saga that will be injected
    -   `params.mode` **[string][26]?** The injection behaviour to use. The default is
        `SagaInjectionModes.DAEMON` which causes the saga to be started on component
        instantiation and never canceled or started again. @see
        [SagaInjectionModes][22] for the other possible modes.

#### Examples

```javascript
class BooksManager extends React.PureComponent {
 render() {
   return null;
 }
}

export default injectSaga({ key: "books", saga: booksSaga })(BooksManager)
```

### useInjectSaga

A react hook that dynamically injects a saga when the hook is run

#### Parameters

-   `params` **[Object][24]** 
    -   `params.key` **[string][26]** The key to inject the saga under
    -   `params.saga` **[function][25]** The saga that will be injected
    -   `params.mode` **[string][26]?** The injection behaviour to use. The default is
        `SagaInjectionModes.DAEMON` which causes the saga to be started on component
        instantiation and never canceled or started again. @see
        [SagaInjectionModes][22] for the other possible modes.

#### Examples

```javascript
function BooksManager() {
  useInjectSaga({ key: "books", saga: booksSaga })

  return null;
}
```

## Misc




### forceReducerReload

Forces a reload of the injected reducers. i.e. Causes `createReducer` to be
called again with the injected reducers. Useful for hot-reloading.

#### Parameters

-   `store`  The redux store that has been configured with
                     `createInjectorsEnhancer`

#### Examples

```javascript
forceReducerReload(store);
```

### SagaInjectionModes

An enum of all the possible saga injection behaviours

#### Properties

-   `RESTART_ON_REMOUNT` **[String][26]** The saga will be started on component instantiation and cancelled with
    `task.cancel()` on component unmount for improved performance.
-   `DAEMON` **[String][26]** Causes the saga to be started on component instantiation and never canceled
    or started again.
-   `ONCE_TILL_UNMOUNT` **[String][26]** Behaves like 'RESTART_ON_REMOUNT' but never runs it again.

[1]: #setup

[2]: #createinjectorsenhancer

[3]: #parameters

[4]: #examples

[5]: #injectors

[6]: #injectreducer

[7]: #parameters-1

[8]: #examples-1

[9]: #useinjectreducer

[10]: #parameters-2

[11]: #examples-2

[12]: #injectsaga

[13]: #parameters-3

[14]: #examples-3

[15]: #useinjectsaga

[16]: #parameters-4

[17]: #examples-4

[18]: #misc

[19]: #forcereducerreload

[20]: #parameters-5

[21]: #examples-5

[22]: #sagainjectionmodes

[23]: #properties

[24]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[25]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String