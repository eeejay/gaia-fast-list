[![](https://travis-ci.org/fxos-components/gaia-fast-list.svg)](https://travis-ci.org/fxos-components/gaia-fast-list) [![Coverage Status](https://coveralls.io/repos/fxos-components/gaia-fast-list/badge.svg?branch=master&service=github)](https://coveralls.io/github/fxos-components/gaia-fast-list?branch=master)

## Installation

```bash
$ bower install fxos-components/gaia-fast-list
```

## Usage

```html
<gaia-fast-list>
  <template>
    <li>
      <h3>${title}</h3>
      <p>${body}</p>
    </li>
  </template>
</gaia-fast-list>
```

```js
var list = document.querySelector('gaia-fast-list');

// triggers render
list.setModel([
  { title: 'Title 1', body: 'Body 1' },
  { title: 'Title 2', body: 'Body 2' },
  { title: 'Title 3', body: 'Body 3' },
  ...
);
```

## Sections

To group list-items into sections, define a `getSectionName()` function before assigning a `model`.

```js
list.configure({
  getSectionName: function(item) {
    return item.section;
  }
});

list.setModel([
  { title: 'Title 1', body: 'Body 1', section: 1 },
  { title: 'Title 2', body: 'Body 2', section: 1 },
  { title: 'Title 3', body: 'Body 3', section: 2 },
  ...
];
```

## Images

GaiaFastList takes care of rendering images for you to ensure that scrolling performance remains fast.

Place `<div class="image"><img/></div>` as the *first* child of your list-item template.

```html
<gaia-fast-list>
  <template>
    <li>
      <div class="image"><img/></div>
      <h3>${title}</h3>
      <p>${body}</p>
    </li>
  </template>
</gaia-fast-list>
```

Then define a `.getItemImageSrc()` function that returns either a `String` or a `Blob`, sync or async (by returning a `Promise`).

```js
list.configure({
  getItemImageSrc(item) { return item.src; }
});
```

## Caching

The optional caching feature will cache rendered list-items and section HTML in `localStorage`. On second render we inject the cached HTML right away for a really fast first-paint. This way the user see some content right away, giving you time to fetch your model behind the scenes.

```html
<gaia-fast-list caching>
  <template>
    ...
  </template>
</gaia-fast-list>
```

```js
list.setModel([...]);

// update the cached content
list.cache();

// you can clear caches if need be
list.clearCache();
```

## Optimizing reflows

Defining `top` and `bottom` offsets avoids the component having to read dimensions from the DOM, which can be costly. The following example is for a list that occupies the entire vertical screen space.

```html
<gaia-fast-list top="0" bottom="0">
  <template>
    ...
  </template>
</gaia-fast-list>
```

## Offsetting content

Sometimes you may require elements other than list-items within your scrollable region (eg. a search field). The `offset` attribute allows you to define a value which all list content will be offset by. The value should usually be the height of your 'foreign' element.

```html
<gaia-fast-list offset="50">
  <div style="height: 50px"></div>
  <template>
    ...
  </template>
</gaia-fast-list>
```

## Tests

1. Ensure Firefox Nightly is installed on your machine.
2. `$ npm install`
3. `$ npm test`

If your would like tests to run on file change use:

`$ npm run test-dev`

## Lint check

Run lint check with command:

`$ npm run lint`
