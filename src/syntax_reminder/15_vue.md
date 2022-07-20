<!-- markdownlint-disable MD001 -->

# Vue

- [Template](#template)
- [Directives](#directives)
- [Input binding](#input-binding)
- [Event handling](#event-handling)
- [Component](#component)
- [API](#api)
  - [Class API](#class-api)
  - [Options API](#options-api)
  - [Component API](#composition-api)
- [i18n (component interpolation)](#i18n-component-interpolation)

### Template

```html
<div id="myApp">  
    {{ message }}  
</div>
```

### Directives

```html
<div v-if="isVisible"></div>
<div v-once>{{ permanent message}}</div>
<div v-bind:class="{ 'is-active': isActive }"></div>
<input v-model="message">  <!-- two way data binding -->
<button v-on:click="doSomething"></button>

 <!-- Dynamic argument -->
<a v-bind:[attributeName]="url"></a>

 <!-- Modifier -->
 <form v-on:submit.prevent="onSubmit"></form> <!-- call event.preventDefault() -->

<!-- Shorthand -->
<div :class="{ 'is-active': isActive }"></div> 
<button @click="doSomething"></button>
```

```javascript
var app = new Vue({  
    el: '#app',  
    data: {  
        isVisible: true,
        isActive: false,
    }  
})
```

### Input binding

```html
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

### Event handling

```html
<button v-on:click="myClickHandler">Click me!</button>  
```

```javascript
var app = new Vue({  
    el: '#app',  
    methods: {  
        myClickHandler: (event) => {  
            console.log('Button clicked!');  
        }  
    }  
})
```

### Component

```javascript
Vue.component('my-component-name', {
    el: '#app',
    data: {},
    props: {}
    computed: {},
    methods: {
        // Do not use an arrow function to define a method
        myMethod: function () {}
    },
    mounted: function () {},
    beforeDestroy: function () {},
})
```

```html
<my-component-name />
```

### API

#### Class API

``` javascript
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class PageIndex extends Vue {
  message: string = "This is a message";
}
</script>
```

#### Options API

``` javascript
<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data() {
    const message: string = "This is a message";

    return {
      message,
    };
  },
});
</script>
```

#### Composition API

``` javascript
<script lang="ts">
import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  setup() {
    const message = ref("This is a message");

    return {
      message,
    };
  },
});
</script>
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
export default Vue.extend({
  i18n: {
    messages: {
      de: {
        paragraph: {
          text: "This is my {my-slot}.",
          link: "My url",
        },
      }
    }
  }
```
