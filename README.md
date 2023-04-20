# components_demo

## Project Setup & Node Package Manager(npm)
#### Install libraries `npm install` (As long as package.json is present, can install node_modules)
#### Start server `npm run serve`
#### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Vue.js Structure
### A single page application
Vue has below three parts :
  - `<template></template>` : includes html code and also css class using className
  - `<script></script>` : import
  - `<style></style>`
### `App.vue` : master/parent component
```vue
<template>
  <div className='App'>
    <div className="programs">
      <label> Remaining UG Seats : {{ ugSeats }}</label>
      <br><br>
      <label> Remaining PG Seats : {{ pgSeats }}</label>
      <br><br>
      <label>Choose Program: </label>
      <select className="appDropDowns" v-model="program">
        <option value="UG">Undergraduate</option>
        <option value="PG">Postgraduate</option>
      </select>
      <br><br>
    </div>
    <div>
      <EnrolmentForm :chosenProgram="program" 
      :currentSeats="program === 'UG' ? ugSeats : pgSeats"
      :setUpdatedSeats="setUpdatedSeats"
      :setStudentDetail="setStudentDetail"/>
    </div>
    <div>
      <EnrolList :studentDetail="studentDetail" />
    </div>
  </div>
</template>

<script>
import './App.css';
import EnrolmentForm from './components/EnrolmentForm.vue';
import EnrolList from './components/EnrolList.vue';

export default {
  name: 'App',
  components: {
    EnrolmentForm,
    EnrolList
  },
  data() {
    return {
      program: "UG",
      ugSeats: 60,
      pgSeats: 40,
      studentDetail : {} //empty object
    };
  },
  methods: {
    setStudentDetail(studentDetail) {
      this.studentDetail = studentDetail;
    },

    setUpdatedSeats(updatedSeats) {
      if(this.program === 'UG') {
        this.ugSeats = updatedSeats;
      } else {
        this.pgSeats = updatedSeats;
      }
    }
  }
}
</script>

<style></style>
```

### `EnrolmentForm.vue` : child component
- v-model enables changed values to be saved in stage variables (fname, lname)

```vue
<template>
    <div>
        <form className='enrolForm'>
            <h1>{{ chosenProgram }} Student Details</h1>
            <label>First name:</label>
            <input type="text" name="fname" v-model="fname"/>
            <br />
            <label>Last name:</label>
            <input type="text" name="lname" v-model="lname"/>
            <br />
            <br />
            <input type='submit' value='Enrol' @click="handleSubmit" />
            <br />
            <br />
            <label id="studentMsg" className="message">{{ welcomeMessage }}</label>
        </form>
    </div>
</template>

<script>
import '../App.css';

export default {
    name: 'EnrollmentForm',
    props: ['chosenProgram', 'currentSeats', 'setUpdatedSeats', 'setStudentDetail'],
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
            let newStudent = {
                fname: this.fname,
                lname: this.lname,
                program: this.chosenProgram
            }
            this.setStudentDetail(newStudent);
            this.fname = "";
            this.lname = "";
        }
    }
}
</script>

<style scoped></style>

```

### `EnrolList.vue` : child component
```vue
<template>
  <div>
    <h1>Student List</h1>
    <ul v-if="items.length">
      <li v-for="item in items" :key="item.id"> 
        Student Details : {{ item.fname }} {{ item.lname }} {{ item.program }}
      </li>
    </ul>
    
  </div>
</template>

<script>
import '../App.css';
export default {
  name: 'EnrolList',
  props: {
    studentDetail : {
      fname: "",
      lname: "",
      program: ""
    }
  },
  data() {
    return {
      items: []
    }
  },
  watch: { 
    //this method will be automatically executed when there is any change in studentDetail
    studentDetail(newStudent) {
      this.items.push(newStudent);
      //this.items = [...this.items, newStudent];
    },
  }
}
</script>

<style sco
```

## Establish communications between components

- Parent (App.vue) to Child (EnrolmentForm.vue) | Parent (App.vue) to Child (EnrolList.vue) via props. 
  Props pass variables or functions to the child component
  EnrolmentForm
  - :chosenProgram="program" 
    transport either "UG" or "PG" defined by "program" vaiable to child component to change title
  - :currentSeats="program === 'UG' ? ugSeats : pgSeats" 
    selected program will be saved in each variable
  - :setUpdatedSeats="setUpdatedSeats" 
  - :setStudentDetail="setStudentDetail"
  EnrolList
  - :studentDetail="studentDetail"
  
- Child (EnrolmentForm.vue) to Parent (App.vue) via callback functions as props
  callback functions : setUpdatedSeats, setStudentDetail
  - functions are defined and executed in parent as they are called from child component
 
- Siblings (EnrolmentForm.vue - EnrolList.vue) via parent component, cannot communicate directly.
  - Displays studentDetail
  - **Conditional Rendering** displays the data based on some conditions
  ```vue
  <ul v-if="items.length">
    <li v-for="item in items" :key="item.id">
      Student Details : {{ item.fname }} {{ item.lname }} {{ item.program }}
    </li>
  </ul>
  ```
