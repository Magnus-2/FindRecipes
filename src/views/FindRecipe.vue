<template>
    <div class="row">
        <h2>SignUp</h2>
        <div class="col-xs-3 col-sm-3 col-md-3 col-lg-3 col-md-offset-3"/>
        <div class="col-xs-6 col-sm-6 col-md-6 col-lg-6 col-md-offset-3">

            <!--Zutaten sollen ausgewählt werden können mit Buttons oder Dropdown Menü?-->

            <button @click="signUp" class="btn btn-success">SignUp</button>
        </div>
    </div>
</template>
<script>

export default {
  name: 'FindRecipe',
  data () {
    return {
      recipeData: {
        recipe: null,
        recipes: {},
        recipeId: {},
      }
    }
  },
  methods: {
     findRecipes(){} //search for Ingredients
     //retreive the Recipe_ID from Recipe_Ingredients where Recipe_Ingredients.Ingredient_Name == Entry_Ingredient_Name
     //--> for every entered Ingredient
     //display every recipe with the found Recipe_ID like in RecipeList with Routerlink to Info about Recipe like in RecipeList

  }
}
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