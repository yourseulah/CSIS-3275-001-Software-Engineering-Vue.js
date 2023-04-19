# components_demo

## Project Setup & Node Package Manager(npm)

#### Install libraries `npm install` (As long as package.json is present, can install node_modules)

#### Start server `npm run serve`

#### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

## Vue.js Structure

### A single page application

### `App.vue` : master/parent component

- `<template></template>` : includes html code and also css class using className
- `<script></script>` : import
- `<style></style>`

### `EnrolmentForm.vue` : child component
- v-model enables changed values to be saved in stage variables (fname, lname)

```vue
<template>
  <div>
    <form className="enrolForm">
      <h1>Student Details</h1>
      <label>First name:</label>
      <input type="text" name="fname" v-model="fname" /> 
      //v-model enables changed values to be saved in stage variables
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
  props: ['chosenProgram'], //props declared
  data() {
    return {
      //stage variables
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

- Parent (App.vue) to Child (EnrolmentForm.vue) via props. 
  Props pass variables or functions to the child component
  - :chosenProgram="program" 
    transport either "UG" or "PG" defined by "program" vaiable to child component to change title
  - :currentSeats="program === 'UG' ? ugSeats : pgSeats" 
    selected program will be saved in each variable
  - :setUpdatedSeats="setUpdatedSeats" 
    function is defined and executed in parent and setUpdatedSeats prop carrying setUpdateSeats will be called in child component
  ```vue
    <div>
      <EnrolmentForm :chosenProgram="program" 
      :currentSeats="program === 'UG' ? ugSeats : pgSeats"
      :setUpdatedSeats="setUpdatedSeats"/>
    </div>
  ```
  - methods
  ```vue
    methods: {
    setUpdatedSeats(updatedSeats) {
      if(this.program === 'UG') {
        this.ugSeats = updatedSeats;
      } else {
        this.pgSeats = updatedSeats;
      }
    }
  }
  ```
- Child (EnrolmentForm.vue) to Parent (App.vue) cannot use props. 
  Calls setUpdatedSeats() function defined in parent and the execution is done in parent 
  ```vue
  export default {
    name: 'EnrollmentForm',
    props: ['chosenProgram', 'currentSeats', 'setUpdatedSeats'],
    data() {
        return {
            //stage variables
            welcomeMessage: "",
            fname: "",
            lname: ""
        }
    },
    methods: {
        handleSubmit(event) {
            event.preventDefault();
            this.welcomeMessage = `Welcome ${this.fname} ${this.lname}`;
            this.setUpdatedSeats(this.currentSeats - 1);
        }
    }
  }
  ```
    
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
