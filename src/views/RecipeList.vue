<template>
    <div class="recipelist">
      <h4>Recipe List</h4>
      <br>
      <div class="row">
      <div class="col-xs-2 col-sm-2 col-md-2 col-lg-2"/>
      <div class="col-xs-8 col-sm-8 col-md-8 col-lg-8">
      <div class="panel panel-info" >
        <div class="panel-heading">
          <h3 class="panel-title">List of Recipes</h3>
        </div>
        <div class="panel-body">
          <div class="row">
        <div class="col-sm-6 col-md-4" v-for="(recipe, key) in recipes" :key = 'key' >
        
          <div class="thumbnail">
            <img src="" width=80%>
            <div class="caption">
              <p><b>Recipe Name</b></p>
              <p class="recipename">{{recipe.Recipe_Name}}</p>
              
              <router-link :to = "{path: 'info', name: 'Info', params:{recipe:recipe.Recipe_Name}}">
              <button class="btn btn-success" role="button">Detail</button>
             </router-link>
            </div>
        
          </div>
        </div>
      </div>
        </div>
      </div>
      </div>
      <div class="col-xs-2 col-sm-2 col-md-2 col-lg-2"/>
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
    name: 'RecipeList',
    data () {
      return {
        recipe: null,
        recipes: {},
       
        
        auth: getAuth()
      }
    },
    mounted () {
      console.log('Recipe List')
      const db = getFirestore()
      const colRef = collection(db, "Recipe")
      onSnapshot(colRef, snapShot => {
        this.recipes = snapShot.docs.map(doc => doc.data())
        
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