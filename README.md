# hyperapp-unite
> A utility function for merging reducers, effects and routes with safe namespacing

## Install

```
npm i -S hyperapp-unite
```

## Usage

```
import { uniteActions } from 'hyperapp-unite'

const x = {
  inc: model => ({ x: model.x + 1 })
  dec: model => ({ x: model.x - 1 })
}

const y = {
  inc: model => ({ y: model.y + 1 })
  dec: model => ({ y: model.y - 1 })
}

export default uniteActions({ x, y })
```

The above code will export an object with every reducer action namespaced using its parents key (`x`,`y`) as a  camel case suffix:

```
{
  incX: f(model)
  decX: f(model)
  incY: f(model)
  decY: f(model)
}
```

This object can be passed in to hyperapp as the `update` or `effects` value..

```
import reducers from './reducers'
app({
  update: reducers,
  model: { x:0, y:0 }
  view: (_, actions) =>
    <button onClick={e => actions.incX()}>X+<button>
    <button onClick={e => actions.incY()}>Y+<button>
})
```
