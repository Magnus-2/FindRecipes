<template>
    <div class="profile">
      <h4>City List</h4>
      <br>
      <div class="row">
      <div class="col-xs-8 col-sm-8 col-md-8 col-lg-8">
      <div class="panel panel-info" >
        <div class="panel-heading">
          <h3 class="panel-title">List of Recipes</h3>
        </div>
        <div class="panel-body">
          <div class="row">
        <div class="col-sm-6 col-md-4" v-for="(user, key) in users" :key = 'key' >
          <div class="thumbnail">
            <img src="" width=80%>
            <div class="caption">
              <p><b>Username</b></p>
              <p class="Profile">{{user.Username}}</p>
              <p class="Email">{{user.Email}}</p>
              <p class="Profile">{{user.Diet}}</p>
              <p class="Profile">{{user.Password}}</p>
              <!--Favoriten müssen auch aufgelistet werden-->
              
              
            </div>
          </div>
        </div>
      </div>
        </div>
      </div>
      </div>
      </div>
      <div class="row">
      <div class="container">
        <button @click="logout" class="btn btn-default"><span class="glyphicon glyphicon-log-out"></span> Logout</button>
      </div>
      </div>
      <br>
    </div>
  </template>
  
  <script>
  import {collection, onSnapshot, doc, getFirestore, } from "firebase/firestore"
  import {getAuth, signOut} from 'firebase/auth'
  export default {
    name: 'Profile',
    data () {
      return {
        user: null,
        users: {},
        userIds:{},
        auth: getAuth()
      }
    },
    mounted () {
      console.log('This is the User Profile')
      const db = getFirestore()
      const colRef = collection(db, "User")
      onSnapshot(colRef, snapShot => {
        this.users = snapShot.docs.map(doc => doc.data())
        this.userIds = snapShot.docs.map(doc => doc.id)
      })
    },
    methods: {
      logout () {
        console.log('logout')
        signOut(this.auth)
      .then(()=>{
        this.$router.replace('/signin')
      })
      .catch((error) => {
        alert(error.message)
      })
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    /* display: inline-block; */
    margin: 0 10px;
  }
  a {
    color: #ffffff;
  }
  p.citydetail{
    text-align: justify;
  }
  </style>