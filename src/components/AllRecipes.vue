<template>
    <header>
        <h3>All Recipes</h3>
    </header>
    <section>
        <button @click="getAllRecipes">Load Recipes</button>
        <ul>
            <li v-for="recipe in recipes" :key="recipe.id">
                <the-recipe>
                    <div>
                        <span>Recipe: </span>
                        <span>{{ recipe.name }}</span>
                    </div>
                    <div>
                        <span>Ingredients: </span>
                        <span>{{ recipe.ingredients }}</span>
                    </div>
                </the-recipe>
            </li>
        </ul>
    </section>
</template>

<script>
import TheRecipe from './TheRecipe.vue';
export default {
    components: {
        TheRecipe,
    },
    data() {
        return {
            recipes: [],
        };
    },
    methods: {
        getAllRecipes() {
            fetch(
                'https://simple-recipe-app-89356-default-rtdb.firebaseio.com/Recipes.json'
            )
                .then((response) => {
                    if (response.ok) {
                        return response.json();
                    }
                })
                .then((data) => {
                    const recipes = [];
                    for (const id in data) {
                        recipes.push({
                            id,
                            name: data[id].name,
                            ingredients: data[id].ingredients[0],
                        });
                        this.recipes = recipes;
                    }
                });
        },
    },
    mounted() {
        this.getAllRecipes();
    },
};
</script>

<style scoped>
ul li {
    list-style: none;
}
</style>
