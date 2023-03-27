<template>
  <div>
    <h1>Student List</h1>
    <!-- in template no need for this. {{ this.studentDetail.fname }} -->
    {{ studentDetail.fname }} {{ studentDetail.lname }} {{ studentDetail.program }} 
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
  }
}
</script>

<style scoped>
</style>