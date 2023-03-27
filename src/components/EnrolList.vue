<template>
  <div>
    <h1>Student List</h1>
    <ul v-if="items.length">
      <li v-for="item in items" :key="item.id">
        Student Details : {{ item.fname }} {{ item.lname }} {{ item.program }}
      </li>
    </ul>
    <!-- in template no need for this. {{ this.studentDetail.fname }} -->
    <!-- {{ studentDetail.fname }} {{ studentDetail.lname }} {{ studentDetail.program }}  -->
  </div>
</template>

<script>
import '../App.css';

export default {
  name: 'EnrolList',
  props: {
    studentDetail: {
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

  //watch dog: keep monitoring your page
  watch: {
    //this method will be automatically executed when there is any change in the student detail
    studentDetail(newStudent) {
      // this.items.push(newStudent);
      this.items = [...this.items, newStudent];
    }
  }
}
</script>

<style scoped>
</style>