<template>
    <div class="Info">
      <div>
    
      
      <div class="col-xs-8 col-sm-8 col-md-8 col-lg-8">
        <div class="panel panel-info" >
            <div class="panel-heading">
              <h3 class="panel-title">Recipe Name</h3>
            </div>
            <div class="panel-body">
              <div class="row">
                
              
              
         </div>
        
        <div class="col-sm-6 col-md-4" v-for="(recipe, key) in recipes" :key = 'key' >
        
          <div class="thumbnail">
            <img src="" width=80%>
            <div class="caption">
              <p><b>Recipe Name</b></p>
              <p class="recipename">{{recipe.Recipe_Name}}</p>
              <p class="recipeID">{{recipeId}}</p>

              <p class="totalcalories">Total kcal:{{recipe.Total_kcal}}kcal</p>
              <p class="totalproteins">Proteins:{{recipe.Total_Protein}}g</p>
              <p class="totalfats">Fats:{{recipe.Total_Fats}}g</p>
              <p class="totalcarbs">Carbs:{{recipe.Total_Carbs}}g</p>
              <p class="servings">Servings:{{recipe.Servings}}</p>
              <p class="style">Style:{{recipe.Style}}</p>
              <p class="ingredients">Ingredients:{{this.ingredients}}</p>
              <p class="instructions">Instructions:{{recipe.Instructions}}</p>
              
            </div>
        </div>
    </div>
                   
                </div>
              </div>
              <div class="row">
                <img :src="``" alt=""><!--here we have to access the database to retrieve the picture-->
              </div>
            </div>
          
      </div>
    
      <div class="col-xs-2 col-sm-2 col-md-2 col-lg-2"/>
      <p><b>Author:</b> </p>
      </div>
      
    </template>
    <script>
    import {where, query, collection, onSnapshot, doc, getFirestore, getDocs} from "firebase/firestore"


    
    export default {
      name: 'Recipe',
      data () {
        return {
        recipe: this.$route.params.recipe,
        recipes: {},
        recipeId:{},
        ingredients:[],
        recipeIngredient: null,
        recipeIngredients: {},
        userIds:{},

      }
    
        }
      ,
      mounted () {
      console.log('Recipe Info')
      const db = getFirestore()
      const colRef = collection(db, "Recipe")

      
      onSnapshot(colRef, snapShot => {
        this.recipes = snapShot.docs.map(doc => doc.data())
        this.recipeId = snapShot.docs.map(doc => doc.id)
        this.getIngredients()
       
      })
      
      
    },
    
  methods: {
    async getIngredients() {
        console.log("getting ingredients")
      const db = getFirestore()
      const q = query(collection(db, 'Recipe_Ingredient'), where('Recipe_ID', '==', this.recipeId))
      console.log(this.recipeId)
      const querySnap = await getDocs(q);

      querySnap.forEach((doc) => {
        this.ingredients.push(doc.data())
      })
      console.log("these are the ingredients:"+this.ingredients)

    },
    async setFavorite(){
      console.log("getting User_ID")
      const dbUser = getFirestore()
      const colRefUser = collection(dbUser, "User")
      onSnapshot(colRefUser, snapShot => {
        this.userIds = snapShot.docs.map(doc => doc.id)
      })
      console.log(this.userIds)
      console.log("setting recipe as a favorite")
      const db = getFirestore()
      const q = query(collection(db, 'Favorites'))
      onSnapshot(q, snapShot => {
        
      })

    }
      
  }}
    </script>
    <style scoped>
    p{
      text-align: left;
    }
    </style>