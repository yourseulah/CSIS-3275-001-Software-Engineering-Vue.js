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
            <input type='submit' value='Enroll' @click="handleSubmit" />
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
            //whenever user changes the input, value typed is saved in below stage variables
            //v-model enables it.
            welcomeMessage: "",
            fname:"",
            lname:""
        }
    },
    methods: {
        
        handleSubmit(event) {
            event.preventDefault(); //disallow default event in the webpage when user clicks submit btn, won't submit form
            this.welcomeMessage = `Welcome ${this.fname} ${this.lname}`; //backtick, NOT single quote
            this.setUpdatedSeats(this.currentSeats -1);
            
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

<style scoped>
</style>
