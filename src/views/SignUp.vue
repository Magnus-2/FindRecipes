<template>
    <div class="row">
        <h2>SignUp</h2>
        <div class="col-xs-3 col-sm-3 col-md-3 col-lg-3 col-md-offset-3"/>
        <div class="col-xs-6 col-sm-6 col-md-6 col-lg-6 col-md-offset-3">

            <input type="email" class="form-control" placeholder="email" v-model="formData.email">
            <br>
            <input type="password" class="form-control" placeholder="password" v-model="formData.password">
            <br>
            <input type="username" class="form-control" placeholder="Username" v-model="formData.username">
            <br>
            <input type="diet" class="form-control" placeholder="Diet: omnivore/vegan/vegetarian/halal" v-model="formData.diet">
            <br> 
           <!-- we need a dropdown menu where a user can choose if he is omnivore, vegetarian, vegan or halal)-->

            <button @click="signUp() " class=" btn btn-success " >SignUp</button>
        </div>
    </div>
</template>
<script>
import{getAuth, createUserWithEmailAndPassword} from "firebase/auth"
import {getFirestore, doc} from 'firebase/firestore'
export default {
  name: 'SignUp',
  data () {
    return {
      formData: {
        email: '',
        password: '',
        username:'',
        diet:'',
      }
    }
  },
  methods: {
    signUp () {
      console.log('SignUp')
      const auth = getAuth()
            createUserWithEmailAndPassword(
                auth,
                this.formData.email,
                this.formData.password
            )
            .then((userCredential)=>{
                console.log("Successfully registered!")
                this.$router.replace('/recipes')
            })
            .catch((error) => {
                console.log(error.code)
                alert(error.message)
            })
            
        }/*, 
        addUser soll die USer zur Datenbank hinzufügen um Speichern von Fvoriten zu ermöglichen
       addUser(){
           const db = getFirestore()
           const colRef = doc(collection(db,"User"))
           const dataObj = {Email: this.email, Diet: this.diet, Username: this.username};
           setDoc(colRef,dataObj)
           .then(docRef => {
            console.log("Document has been added successfully")
})
          .catch(error => {
          console.log(error);
})
        
}*/
}}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>