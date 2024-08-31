<!-- markdownlint-disable MD001 -->

# Vue

- [Template](#template)
- [Directives](#directives)
- [Component](#component)
- [Prop binding](#prop-binding)
- [Event handling](#event-handling)
- [Input binding](#input-binding)
- [API](#api)
  - [Class API](#class-api)
  - [Options API](#options-api)
  - [Component API](#composition-api)
- [i18n (component interpolation)](#i18n-component-interpolation)

### Template

```html
<p>{{ message }}</p> <!-- text interpolation -->
```

### Directives

```html
<div v-if="isVisible"></div> <!-- conditional rendering -->
<div v-for="item in items">{{ item }}</div> <!-- render list of items -->
<div v-once>{{ message }}</div> <!-- render once -->

<div v-bind:class="{ 'is-active': isActive }"></div> <!-- class binding -->
<div :class="{ 'is-active': isActive }"></div>  <!-- class binding (shorthand) -->

<button v-on:click="doSomething"></button> <!-- event listener -->
<button @click="doSomething"></button> <!-- event listener (shorthand) -->

<input v-model="message">  <!-- two way data binding -->

 <!-- Dynamic argument -->
<a v-bind:[attributeName]="url"></a>

 <!-- Modifier -->
 <form v-on:submit.prevent="onSubmit"></form> <!-- call event.preventDefault() -->
```

### Component

```javascript
import MyChildComponent from './my-child-component.vue'

export default {
    name: 'my-component-name',
    components: { MyChildComponent },
    data: {},
    props: {}
    computed: {},
    methods: {
        // Do not use an arrow function to define a method
        myMethod: function () {}
    },
    mounted: function () {},
    beforeDestroy: function () {},
}
```

```html
<my-component-name />
```

### Prop binding

Parent component:

``` html
<template>
  <MyChildComponent :child-message="parentMessage" />
</template>
```

``` javascript
export default {
  components: { MyChildComponent },
  data() {
    const parentMessage: string = "My parent message.";

    return { parentMessage };
  },
};
```

Child component:

``` javascript
export default {
  props: {
    childMessage: String,
  },
};
```

### Event handling

```html
<button v-on:click="myClickHandler">Click me!</button>  
```

```javascript
export default {
  methods: {
    myClickHandler: (event) => {
      console.log("Button clicked!");
    },
  },
};
```

### Input binding

```html
<input v-model="message">
<p>Message is: {{ message }}</p>
```

### API

#### Class API

``` javascript
import { Component, Vue } from "vue-property-decorator";

@Component
export default class MyComponent extends Vue {
  message: string = "This is a message";
}
```

#### Options API

``` javascript
import Vue from "vue";

export default Vue.extend({
  data() {
    const message: string = "This is a message";

    return {
      message,
    };
  },
});
```

#### Composition API

``` javascript
import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  setup() {
    const message = ref("This is a message");

    return {
      message,
    };
  },
});
```

### i18n (component interpolation)

```html
<i18n path="paragraph.text" tag="p">
  <template v-slot:my-slot>
    <a href="https://example.com">{{ $t("paragraph.link") }}</a>
  </template>
</i18n>
```

```javascript
export default {
  i18n: {
    messages: {
      de: {
        paragraph: {
          text: "This is my {my-slot}.",
          link: "My url",
        },
      },
    },
  },
};
```
