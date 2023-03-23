<template>
    <div class="Info">
      <div>
    
      
      <div class="col-xs-8 col-sm-8 col-md-8 col-lg-8">
        <div class="col-sm-6 col-md-4" v-for="(recipe, key) in recipes" :key = 'key' >
        <div class="panel panel-info" >
            <div class="panel-heading">
              <h3 class="panel-title"> {{ recipe.Recipe_Name }}</h3>
            </div>
            <div class="panel-body">
              <div class="row">
                
              
              
         </div>
         
        
          

          
        
        
          <div class="thumbnail">
            <img src="" width=80%>
            <div class="caption">
            
              <img :src="`../src/assets/${recipe.image}`" style="width: 200px"/><!--here we have to access the database to retrieve the picture-->

              <p class="totalcalories">Total kcal:{{recipe.Total_kcal}}kcal</p>
              <p class="totalproteins">Proteins:{{recipe.Total_Protein}}g</p>
              <p class="totalfats">Fats:{{recipe.Total_Fats}}g</p>
              <p class="totalcarbs">Carbs:{{recipe.Total_Carbs}}g</p>
              <p class="servings">Servings:{{recipe.Servings}}</p>
              <p class="style">Style:{{recipe.Style}}</p>
              <p class="ingredients">Ingredients:</p>
              <div v-for="(ingredientDetail, index) in ingredientDetails" :key="index">
              <p class="ingredients_values">{{ ingredients[index].Ingredient_Name }}
                {{ ingredients[index].Quantity }}
                {{ ingredientDetail.Unit }}
              </p>
            </div>
              <p class="instructions">Instructions:{{recipe.Instructions}}</p>
            </div>
            
            </div>
        </div>
    </div>
                   
                </div>
              </div>
              <div class="row">
              </div>
            </div>
          
      </div>
    
      <div class="col-xs-2 col-sm-2 col-md-2 col-lg-2"/>
      <div class="col-sm-6 col-md-4" v-for="(recipe, key) in recipes" :key = 'key' >
      <p><b>Author:</b> </p>
      <p>{{ recipe.User_ID_Publisher }}</p>

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
        ingredient: null,
        ingredients:{},
        ingredientIds: {},
        ingredientDetail: null,
        ingredientDetails:{},
        ingredientDetailIds: {},
        users:{},
        user:null

      }
    
        }
      ,
      mounted () {
      console.log('Recipe Info')
      const db = getFirestore()
      const colRefRecipe = collection(db, "Recipe")
      //Aus Recipe_Ingredients sollen nur jene Dokumente abgerufen werden bei denen gilt:
      //ingredients = Recipe_Ingredients.Recipe_ID == this.recipeId
      const colRefRecipe_Ingredients = collection(db,"Recipe_Ingredients")
      // Aus "Ingredient" sollen nur Dokumente abgerufen werden bei denen gilt:
      //(ingredients Array aus vorheriger Abfrage) ingredients.Ingredient_Name == (Datenbank Ingredient) Ingredient.Ingredient_Name
      const colRefIngredients = collection(db,"Ingredient")
      
      onSnapshot(colRefRecipe, snapShot => {
        this.recipes = snapShot.docs.map(doc => doc.data())
        this.recipeId = snapShot.docs.map(doc => doc.id)
        this.users = snapShot.docs.map(doc => doc.data().User_ID_Publisher)
        
       
      })
      console.log("fetching ingredients")
      onSnapshot(colRefRecipe_Ingredients, snapshot => {
      this.ingredients = snapshot.docs.map(doc => doc.data())
      this.ingredientIds = snapshot.docs.map(doc => doc.id)
      console.log(this.ingredients)})

      console.log("fetching ingredient details")
      onSnapshot(colRefIngredients, snapshot => {
      this.ingredientDetails = snapshot.docs.map(doc => doc.data())
      this.ingredientDetailIds = snapshot.docs.map(doc => doc.id)
      console.log(this.ingredientDetails)})
      //get Unit from the document in Ingredient where : Ingredient.Ingredient_Name == Recipe_Ingredient.Ingredient_Name 
      
      
    },
    
  methods: {
     
     setFavorite(){
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