---
title: Redux Toolkit createSlice怎么实现多个slice构成redux state tree
catalog: true
date: 2023-10-26 22:10:46
subtitle:
header-img:
tags:
- Redux Toolkit
categories:
- TECH
- FrontEnd
- Redux
---

## Redux Toolkit - createSlice

[Redux Toolkit - createSlice 官方文档](https://redux-toolkit.js.org/usage/usage-with-typescript#createslice)这里虽然介绍了`createSlice`的使用方法，但是比较简单，如果我有一个比较复杂，层级比较多的redux store，不同层级都用`createSlice`来实现要怎么做呢？

例如 state tree 的结构：

```javascript
const state = {
    config: {
        a : {
            a1: {},
            a2: {},
            a3: {},
        },
        b: {}
    }，
    content: {}
}
```

### selector成功，reducer失败

#### createStore

```javascript
// createStore
const createStore = (extraArgument: ThunkArgument) => {
  const store = configureStore({
    reducer: {
      content: contentReducer,
      config: aTop,  // config state
    },
    middleware: getDefaultMiddleware =>
      // other code
  })
  setupListeners(store.dispatch)
  return store
}
```

#### `./a1/index.tsx`

```javascript
// ./a1/index.tsx
import { createSlice, PayloadAction } from '@reduxjs/toolkit'

export interface A1 {
  enabled: boolean
  a11: string
}

const initialState: A1 = {
  enabled: false,
  a11: '',
}

const A1Slice = createSlice({
  name: 'a1Slice',
  initialState,
  reducers: {
    updateA1Enabled: (state, { payload }: PayloadAction<boolean>) => {
      state.enabled = payload
    },
    updateA11: (state, { payload }: PayloadAction<string>) => {
      state.a11 = payload
    },
  }
})

export const {
  updateA1Enabled,
  updateA11,
} = A1Slice.actions

export default A1Slice.reducer
```

#### `configSlice.tsx`

```javascript
// configSlice.tsx
import type { Reducer } from 'redux'
import { createSlice, PayloadAction, combineReducers } from '@reduxjs/toolkit'
import a1Reducer, from './a1'
import a2Reducer, from './a2'

const aReducer = combineReducers({
  a1: a1Reducer,
  a2: a2Reducer
})

export type AState = ReturnType<typeof aReducer>

export interface A {
  a: AState
}

const initialState: A = {
  a: aReducer(undefined, { type: 'INIT' })
}

const configSlice = createSlice({
  name: 'configSlice',
  initialState,
  reducers: {
    updateConfig: (state, action: PayloadAction<Config>) => {
      return action.payload
    },
    updateA: (state, action: PayloadAction<AState>) => {
      state.a = action.payload
    },
    updatePartialA: (state, action: PayloadAction<Partial<ReturnType<typeof aReducer>>>) => {
      state.a = { ...state.a, ...action.payload }
    }
  }
})

export const { updateConfig, updateA, updatePartialA } = configSlice.actions
export default configSlice.reducer
```

### 成功实现(selector成功，reducer成功)

#### `./reduce-reducers`

```javascript
// ./reduce-reducers
type Action = {
  type: string
}

type Reducer<S> = (state: S, action: Action) => S

export default (...args: Reducer<unknown>[]): Reducer<unknown> => {
  const initialState = typeof args[0] !== 'function' && args.shift()
  const reducers = args

  if (typeof initialState === 'undefined') {
    throw new TypeError(
      'The initial state may not be undefined. If you do not want to set a value for this reducer, you can use null instead of undefined.'
    )
  }

  return (prevState, value, ...args) => {
    const prevStateIsUndefined = typeof prevState === 'undefined'
    const valueIsUndefined = typeof value === 'undefined'

    if (prevStateIsUndefined && valueIsUndefined && initialState) {
      return initialState
    }

    return reducers.reduce(
      (newState, reducer, index) => {
        if (typeof reducer === 'undefined') {
          throw new TypeError(`An undefined reducer was passed in at index ${index}`)
        }

        return reducer(newState, value, ...args)
      },
      prevStateIsUndefined && !valueIsUndefined && initialState ? initialState : prevState
    )
  }
}

```

#### `./combinSlices`

```javascript
// ./combinSlices
import { combineReducers } from '@reduxjs/toolkit'
import type { Reducer } from 'redux'
import reduceReducers from './reduce-reducers'

const combineSlices = (sliceReducer: Reducer, sliceInitialState: object, childSliceReducers: unknown): Reducer => {
  const noopReducersFromInitialState: unknown = Object.keys(sliceInitialState).reduce((prev, curr) => {
    return {
      ...prev,
      [curr]: (s = null) => s
    }
  }, {})

  const childReducers = combineReducers({
    ...(childSliceReducers as object),
    ...(noopReducersFromInitialState as object)
  })

  return reduceReducers(sliceReducer, childReducers as Reducer<unknown>)
}

export default combineSlices

```

#### `configSlice.tsx` version 2

```javascript
// configSlice.tsx
import type { Reducer } from 'redux'
import { createSlice, PayloadAction, combineReducers } from '@reduxjs/toolkit'
import a1Reducer, from './a1'
import a2Reducer, from './a2'
import combineSlices from './combinSlices'

const aReducer = combineReducers({
  a1: a1Reducer,
  a2: a2Reducer
})

export type AState = ReturnType<typeof aReducer>

export interface A {
  a: AState
}

const initialState: A = {
  a: aReducer(undefined, { type: 'INIT' })
}

// -----------------New added part 1-------------
const aSlice = createSlice({
  name: 'aSlice',
  initialState,
  reducers: {}
})
// -----------------New added part 1-------------

const configSlice = createSlice({
  name: 'configSlice',
  initialState,
  reducers: {
    updateConfig: (state, action: PayloadAction<Config>) => {
      return action.payload
    },
    updateA: (state, action: PayloadAction<AState>) => {
      state.a = action.payload
    },
    updatePartialA: (state, action: PayloadAction<Partial<ReturnType<typeof aReducer>>>) => {
      state.a = { ...state.a, ...action.payload }
    }
  }
})

export const { updateConfig, updateA, updatePartialA } = configSlice.actions
export default configSlice.reducer

// -----------------New added part 2-------------
const aCombine = combineSlices(
  aSlice.reducer,
  {},
  {
    a1: a1Reducer,
    a2: a2Reducer
  }
)
const aTop: Reducer<Config> = combineSlices(
  configSlice.reducer,
  {},
  {
    a: aCombine
  }
)
export { aCombine, aTop }
// -----------------New added part 2-------------
```
