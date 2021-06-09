<template>
    <header>
        <h3>Add Recipe</h3>
    </header>
    <section>
        <form @submit.prevent="AddRecipe">
            <div class="form-control">
                <label for="name">Recipe name</label>
                <input type="text" v-model="recipeName" />
            </div>
            <div class="form-control">
                <label for="name">Ingredient</label>
                <input type="text" v-model="ingredients" />
            </div>
            <p v-if="invalidInput">Please fill in all the required fields</p>
            <div class="form-control">
                <button>Add Recipe</button>
            </div>
        </form>
    </section>
</template>

<script>
export default {
    data() {
        return {
            recipeName: '',
            ingredients: '',
            invalidInput: false,
            error: null,
        };
    },
    methods: {
        AddRecipe() {
            const ingredients = [];
            if (!this.recipeName || !this.ingredients) {
                this.invalidInput = true;
                return;
            }

            ingredients.push(this.ingredients.split(','));

            fetch(
                'https://simple-recipe-app-89356-default-rtdb.firebaseio.com/Recipes.json',
                {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        name: this.recipeName,
                        ingredients,
                    }),
                }
            )
                .then((response) => {
                    if (!response.ok) {
                        throw new Error(
                            'A problem occurred in adding the recipe. Please try again later'
                        );
                    }
                })
                .catch((error) => {
                    this.error = error.message;
                });

            this.recipeName = '';
            this.ingredients = '';
        },
    },
};
</script>

<style scoped>
.form-control {
    margin: 0.5rem 0;
}

input[type='text'] {
    display: block;
    width: 20rem;
    margin-top: 0.5rem;
}
</style>
