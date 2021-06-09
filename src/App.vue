<template>
    <div></div>
    <button @click="toggleActiveComponent('all-recipes')">All Recipes</button>
    <button @click="toggleActiveComponent('add-recipe')">Add Recipe</button>
    <keep-alive>
        <component :is="activeComponent"></component>
    </keep-alive>
</template>

<script>
import AllRecipes from './components/AllRecipes.vue';
import AddRecipe from './components/AddRecipe.vue';
export default {
    components: {
        AllRecipes,
        AddRecipe,
    },
    data() {
        return {
            activeComponent: 'all-recipes',
        };
    },
    methods: {
        toggleActiveComponent(component) {
            this.activeComponent = component;
        },
    },
};
</script>
