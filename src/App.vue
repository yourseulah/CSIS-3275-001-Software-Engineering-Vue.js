<template>
    <div className='App'>
      <div className="programs">
      <label> Remaining UG Seats: {{ ugSeats }}</label>
      <br/>
      <br/>
      <label> Remaining PG Seats: {{ pgSeats }}</label>
      <br/>
      <br/>
      <label> Choose Program : </label>
      <select className="appDropDowns" v-model="program"> 
        <option value="UG">Undergraduate</option>
        <option value="PG">Postgraduate</option>
      </select>
    </div>
    <div>
      <!-- sending "program" variable to a child component(EnrolmentForm.vue) via props -->
      <EnrolmentForm :chosenProgram="program" 
        :currentSeats="program === 'UG' ? ugSeats : pgSeats"
        :setUpdatedSeats="setUpdatedSeats"
        :setStudentDetail="setStudentDetail"/>
    </div>
    <div>
      <EnrolList :studentDetail="studentDetail"/>
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
      studentDetail: {} //an empty object
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
  },

  mounted() {

  }


}
</script>

<style></style>
