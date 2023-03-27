<template>
    <div>
        <form className='enrolForm'>
            <h1>{{ chosenProgram }} Student Details</h1>
            <label>First name:</label>
            <input type="text" name="fname" v-model="fname" />
            <br />
            <label>Last name:</label>
            <input type="text" name="lname" v-model="lname"/>
            <br />
            <br />
            <input type='submit' value='Submit' @click="handleSubmit" />
            <br />
            <label id="studentMsg" className="message">{{ welcomeMessage }}</label>
        </form>
    </div>
</template>


<script>
import '../App.css';
export default {
    name: 'EnrollmentForm',
    props: ['chosenProgram', 'currentSeats', 'setUpdatedSeats'],
    data() {
        return {
            //stage variables
            //whenever user changes the input, value typed will be save in below stage variables
            //v-model enables it.
            welcomeMessage: "",
            fname:"",
            lname:""
        }
    },
    methods: {
        //disallow default event in the webpage
        //when user clicks submit button, we don't want to submit the form
        handleSubmit(event) {
            event.preventDefault();
            this.welcomeMessage = `Welcome ${this.fname} ${this.lname}`; //backtick, NOT single quote
            this.setUpdatedSeats(this.currentSeats -1)
        }
    }

}
</script>

<style scoped>
</style>
