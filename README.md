# tune-up

## Required Listening
https://www.youtube.com/watch?v=-wvXgq3UU7c

## Installation
```
npm i --save-dev @vinli/tune-up
```

## vueRules
### `'vue/no-v-html': 'off'`
use responsibly, never v-html user provided data

### `'vue/require-default-prop': 'off'`
default props are great for simple things like Strings and Numbers,
but can add lots of boilerplate if your prop is a Function, Array,
 or Object. So instead of providing a default for these prop types,
make sure references to the these props are fault tolerant.

#### Example
```js
props: {
  myThing: {
    type: Object
  }
},
methods: {
  getSubthings () {
    if (this.myThing.id) {
      axios.get(`/api/v1/things${this.myThing.id}/subthings`)
    }
  }
}
```
This isn't a perfect solution, but cases where there is _not_ a sensible
default (like when have a uuid that's used for network requests)
made us lean this way. It just felt a little more sane
than coding up stuff like: 
```js
props: {
  myThing: {
    type: Object,
    default: () => {
      return {
        name: 'pizza',
        id: 'some_default_id'
      }
    }
  }
},
methods: {
  getSubthings () {
    if (this.myThing.id !== 'some_default_id') {
      axios.get(`/api/v1/things${this.myThing.id}/subthings`)
    }
  }
}
```

### `'vue/no-template-shadow': 'off'`
We've found this hard to respect in practice when using scoped
slots. Maybe we'll change our minds!