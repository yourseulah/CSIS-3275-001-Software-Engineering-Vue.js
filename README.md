# components_demo

## Project Setup & Node Package Manager(npm)

#### Install libraries `npm install` (As long as package.json is present, can install node_modules)

#### Compiles and hot-reloads for development & start server `npm run serve`

#### Compiles and minifies for production `npm run build`

#### Lints and fixes files `npm run lint`

#### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

## Vue.js Structure

### A single page application

### `App.vue` : master component

- `<template></template>` : includes html code and also css class using className
- `<script></script>` : import
- `<style></style>`

### `EnrolmentForm.vue` : child component

- v-model enables changed values to be saved in stage variables

```vue
<template>
  <div>
    <form className="enrolForm">
      <h1>Student Details</h1>
      <label>First name:</label>
      <input type="text" name="fname" v-model="fname" />
      <br />
      <label>Last name:</label>
      <input type="text" name="lname" v-model="lname" />
      <br />
      <br />
      <input type="submit" value="Submit" @click="handleSubmit" />
      <br />
      <label id="studentMsg" className="message">{{ welcomeMessage }}</label>
    </form>
  </div>
</template>

<script>
import "../App.css";
export default {
  name: "EnrollmentForm",
  data() {
    return {
      //stage variables
      //whenever user changes the input, they are saved in below stage variables
      //v-model enables it.
      welcomeMessage: "",
      fname: "",
      lname: "",
    };
  },
  methods: {
    //disallow default event in the webpage
    //when user clicks submit button, we don't want to submit the form
    handleSubmit(event) {
      event.preventDefault();
      this.welcomeMessage = `Welcome ${this.fname} ${this.lname}`; //backtick, NOT single quote
    },
  },
};
</script>

<style scoped></style>
```

### `EnrolList.vue` : child component

## Establish communications between components

- Parent (App.vue) - Child (EnrolmentForm.vue) : via props

  - Updated seats

- Siblings (EnrolmentForm.vue - EnrolList.vue) : cannot communicate directly, make a parent component
  - Displays student detail
  - **Conditional Rendering** displays the data based on some conditions
  ```vue
  <ul v-if="items.length">
    <li v-for="item in items" :key="item.id">
      Student Details : {{ item.fname }} {{ item.lname }} {{ item.program }}
    </li>
  </ul>
  ```
