<template>
    <div></div>
    <keep-alive>
        <component :is="activeComponent"></component>
    </keep-alive>
</template>

<script>
export default {
    data() {
        return {
            activeComponent: 'AllRecipes',
        };
    },
};
</script>
