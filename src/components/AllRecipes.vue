<template>
    <header>
        <h3>All Recipes</h3>
    </header>
    <section>
        <button @click="getAllRecipes">Load Recipes</button>
        <ul class="general-flex-container">
            <li v-for="recipe in recipes" :key="recipe.id">
                <the-recipe>
                    <div>
                        <span>Recipe: </span>
                        <span>{{ recipe.name }}</span>
                    </div>
                    <div>
                        <span>Ingredients: </span>
                        <ul class="ingredient-section">
                            <li
                                v-for="(
                                    ingredient, index
                                ) in recipe.ingredients"
                                :key="recipe.ingredients[ingredient]"
                            >
                                <span class="ingredient">
                                    {{ recipe.ingredients[index] }}
                                </span>
                            </li>
                        </ul>
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

.ingredient-section {
    margin: 2rem 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: start;
}

.ingredient {
    display: inline-block;
    background-color: cyan;
    padding: 0.5rem 0.8rem;
    border-radius: px;
    margin: 0.5rem;
}

.general-flex-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: start;
}
</style>
