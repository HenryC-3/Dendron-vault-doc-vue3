---
id: 807cqsm8xvgb2dghoa1io3y
title: Utility Types
desc: ''
updated: 1660458244093
created: 1660458244093
isDir: false
---
# Utility Types

:::info
This page only lists a few commonly used utility types that may need explanation for their usage. For a full list of exported types, consult the [source code](https://github.com/vuejs/core/blob/main/packages/runtime-core/src/index.ts#L131).
:::

## PropType\<T>

Used to annotate a prop with more advanced types when using runtime props declarations.

- **Example**

  ```ts
  import { PropType } from 'vue'

  interface Book {
    title: string
    author: string
    year: number
  }

  export default {
    props: {
      book: {
        // provide more specific type to `Object`
        type: Object as PropType<Book>,
        required: true
      }
    }
  }
  ```

- **See also:** [[vue3.guide.typescript.options-api#typing-component-props]]

## ComponentCustomProperties

Used to augment the component instance type to support custom global properties.

- **Example**

  ```ts
  import axios from 'axios'

  declare module 'vue' {
    interface ComponentCustomProperties {
      $http: typeof axios
      $translate: (key: string) => string
    }
  }
  ```

  :::tip
  Augmentations must be placed in a module `.ts` or `.d.ts` file. See [[vue3.guide.typescript.options-api#augmenting-global-properties]] for more details.
  :::

- **See also:** [[vue3.guide.typescript.options-api#augmenting-global-properties]]

## ComponentCustomOptions

Used to augment the component options type to support custom options.

- **Example**

  ```ts
  import { Route } from 'vue-router'

  declare module 'vue' {
    interface ComponentCustomOptions {
      beforeRouteEnter?(to: any, from: any, next: () => void): void
    }
  }
  ```

  :::tip
  Augmentations must be placed in a module `.ts` or `.d.ts` file. See [[vue3.guide.typescript.options-api#augmenting-global-properties]] for more details.
  :::

- **See also:** [[vue3.guide.typescript.options-api#augmenting-custom-options]]

## ComponentCustomProps

Used to augment allowed TSX props in order to use non-declared props on TSX elements.

- **Example**

  ```ts
  declare module 'vue' {
    interface ComponentCustomProps {
      hello?: string
    }
  }

  export {}
  ```

  ```tsx
  // now works even if hello is not a declared prop
  <MyComponent hello="world" />
  ```

  :::tip
  Augmentations must be placed in a module `.ts` or `.d.ts` file. See [[vue3.guide.typescript.options-api#augmenting-global-properties]] for more details.
  :::

## CSSProperties

Used to augment allowed values in style property bindings.

- **Example**

  Allow any custom CSS property

  ```ts
  declare module 'vue' {
    interface CSSProperties {
      [key: `--${string}`]: string
    }
  }
  ```

  ```tsx
  <div style={ { '--bg-color': 'blue' } }>
  ```
  ```html
  <div :style="{ '--bg-color': 'blue' }">
  ```

 :::tip
  Augmentations must be placed in a module `.ts` or `.d.ts` file. See [[vue3.guide.typescript.options-api#augmenting-global-properties]] for more details.
  :::
  
  :::info See also
SFC `<style>` tags support linking CSS values to dynamic component state using the `v-bind CSS` function. This allows for custom properties without type augmentation. 

- [[vue3.api.sfc-css-features#v-bind-in-css]]
  :::
