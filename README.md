# storage [![Build Status](https://travis-ci.org/nicholasadamou/storage.svg?branch=master)](https://travis-ci.org/nicholasadamou/storage)

_Have you ever needed to listen to localStorage or sessionStorage to change from within the same tab? Well, you've come to the right place my friend!_

## Getting Started

`storage` is a small function that emits events in the same page and tab that `sessionStorage` and `localStorage` are changed in.

**No dependencies!**
**Much 🔥!**
**Only ~800b!**

## Installation

You can download the package using `npm` with:

`npm install @nicholasadamou/storage --save`

## The Problem

When `localStorage` or `sessionStorage` are changed, a `storage` event is emitted, but it can only be picked up by other open tabs of the same origin. Sometimes you need access to that event in the tab that it was dispatched from, as well.

```js
// Does not work.
window.addEventListener('storage', baz)

localStorage.setItem('foo', 'bar')
```

## The Solution

The solution is `storage`, obviously. 💁🏼

```js
import storage from '@nicholasadamou/storage'

storage('local')

// Like 🎩, it works!
window.addEventListener('local-storage', foo)
```

## The Options

The first argument must be a string, one of: `"local"` or `"session"` to determine which storage you wish to emit events for.

You can pass an options object as the second argument to `storage`. This options object currently supports one property: `eventName`. Setting the `eventName` will allow you flexibility to have different names for different targets, such as `localStorage` and `sessionStorage`.

```js
storage('session', {
  eventName: 'DonaldTrump'
})

window.addEventListener('DonaldTrump', maga)
```

## The Event

As with any event listener, an event is provided to your callback. In this instance, `event` will have two properties: `key`, and `value`. These values represent the storage key that changed and the new value that accompanies the change.

```js
storage('local', {
  eventName: 'DonaldTrump'
})

window.addEventListener('DonaldTrump', (event) => {
 console.log(event);
})

localStorage.setItem('Election 2020 Quote', 'We WON by a lot!!')
// { key: 'foo', value: 'bar' }
```

## License

© Nicholas Adamou.

It is free software, and may be redistributed under the terms specified in the [LICENSE] file.

[license]: LICENSE
