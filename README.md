# Photo Editor

## A fully functional free online Photo Editor (works only in Chromium browsers for now)

![ScreenShot](/screenshot.png)

### What's that?

PhotoEditor is a Vue SPA utilizing [Element Plus](https://element-plus.org/), canvas filters and [Cropperjs]
You can install the core components via npm and use it in your own project.

#### Download and import PhotoEditor

Of course you can download the editor via npm as an esm module. Please remember that PhotoEditor requires Vuex!

```bash
npm i /photoeditor
pnpm add /photoeditor
yarn add /photoeditor
```

- in a no ssr environment (e.g. Vue spa):

```html
<template>
  <div>
    <PhotoEditor />
  </div>
</template>

<script setup>
  import '@livebcdev0603/photoeditor/dist/photo-editor.css';
  import PhotoEditor from '@livebcdev0603/photoeditor';
</script>
```

- in a ssr environment (e.g. Nuxt universal app):

```html
<template>
  <div>
    <client-only placeholder="Loading...">
      <photoEditor />
    </client-only>
  </div>
</template>

<script>
  import '@livebcdev0603/photoeditor/dist/photo-editor.css'
  export default {
    name: 'your component',
    components:
      PhotoEditor: () => {
      return import('@livebcdev0603/photoeditor').PhotoEditor
        });
      },
    },
  };
</script>
```

#### specification

#### props

- clearDataOnDestroy - if true, photoEditor's data in vuex and sessionStorage is cleared when the beforeDestroy hook is called

```html
<photoEditor clearDataOnDestroy />
```

#### events

you can emit to your photoEditor using this.$root.$emit("photoEditor/event", arguments)

- alterphoto - tells the photoEditor to update the photo (apply css filters)

```javascript
window.dispatchEvent(new CustomEvent('photoEditor/alterphoto')); // no arguments
```

- cropperchange - calls a cropperjs method (works only when cropperjs is available)

```javascript
new CustomEvent('photoEditor/cropperchange', detail('cropperjsmethod', [array with arguments]));
new CustomEvent('photoEditor/cropperchange', detail('rotateTo', [20])); //rotates the image to 20 degrees
```

#### Vuex - actions

- updatesettings - changes value of one css filter, in order to see the result call the alterphoto event

```javascript
this.$store.dispatch('photoEditor/updatesettings', { func: cssfiltername, val: value });
```

#### Vuex - mutations

- resetStore - reset the vuex module to its initial state and clear sessionStorage

```javascript
store.commit('photoEditor/resetStore');
```

### Cotributing

Certainly, contributions are welcome. So if you'd like to addfunctionality or simply make it better, go ahead, PRs welcome !:fire::fire::fire:

### Project setup

```
pnpm install
```

### Compiles and hot-reloads for development

```
pnpm run dev
```

### Compiles the example app for production

```
pnpm run build
```

### Compiles and minifies the library for production

```
pnpm run build:lib
```

### Lints and fixes files

```
pnpm run lint
```
