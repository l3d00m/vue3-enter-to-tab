# vue3-enter-to-tab

[![npm package][npm-img]][npm-url]
[![Release](https://github.com/l3d00m/vue3-enter-to-tab/actions/workflows/release.yml/badge.svg)](https://github.com/l3d00m/vue3-enter-to-tab/actions/workflows/release.yml)
[![ci](https://github.com/l3d00m/vue3-enter-to-tab/actions/workflows/ci.yml/badge.svg)](https://github.com/l3d00m/vue3-enter-to-tab/actions/workflows/ci.yml)

A Vue composable to convert the enter key to tab key. Especially useful when using numpads for inputting forms.

This is a fork of [ajomuch92/vue-enter-to-tab](https://github.com/ajomuch92/vue-enter-to-tab) and has been converted from a mixin to a Vue3 composable. It also features new options.

## Install

Requires Vue 3.3 or higher.

```bash
# npm
npm i --save vue3-enter-to-tab
# yarn
yarn add vue3-enter-to-tab
```

## Usage

**Note**: This doesn't work on textarea elements.

### Minimal example with composition API

```vue
<template>
  <div ref="form"></div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useEnterToTab } from 'vue3-enter-to-tab'

// Get ref to the parent element
const form = ref<HTMLElement | null>(null)

useEnterToTab(form)
</script>
```

### Minimal example with options API

The code has not been tested yet and it is recommended to use the composition API instead.

```vue
<template>
  <div ref="form"></div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import { useEnterToTab } from 'vue3-enter-to-tab'

export default defineComponent({
  setup() {
    useEnterToTab(this.$refs.form)
  },
})
</script>
```

### Full example

See documentation below.

```vue
<template>
  <div ref="form">
    <input />
    <input v-prevent-enter-tab />
  </div>
</template>

<script setup lang="ts">
import { useEnterToTab } from 'vue3-enter-to-tab'
import { ref } from 'vue'

const { vPreventEnterTab, isEnterToTabEnabled } = useEnterToTab(form, {
  autoClickButton: false,
  initialState: false,
})
// Read and change the status using that ref
isEnterToTabEnabled.value = true
</script>
```

## API: `useEnterToTab(element, options?)`

### Input `element`

Type: `HTMLElement | null`

The parent element. This is where the event listener will be attached.

Enter key will be converted for all children input of this element, except for those with the `v-prevent-enter-tab` directive and not including `<textarea>`.

### Input `options`

```ts
interface UseEnterToTabOptions {
  autoClickButton?: boolean
  initialState?: boolean
}
```

#### autoClickButton

If the next element is a button, it will be clicked. Activating this has the advantage that it's not necessary to press enter twice to click a button (often to submit the form).

Disable this if you don't want to click buttons automatically and instead just focus them like other inputs.

Default: `true`

#### initialState

Initial state of the function.

Default: `true`

### Output `vPreventEnterTab`

Directive to use in those inputs you want to avoid use enter as tab. Inputs with this directive will act as normal when pressing enter.

### Output `isEnterToTabEnabled`

Ref to read and change the status of the function.

```vue
[npm-img]: https://img.shields.io/npm/v/vue3-enter-to-tab [npm-url]:
https://www.npmjs.com/package/vue3-enter-to-tab
```
