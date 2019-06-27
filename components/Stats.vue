<template>
    <div>
        <ul>
            <li v-for="stat in stats.slice().reverse()"> {{ (stat.stat.name).toUpperCase() }} {{ stat.base_stat }}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        props:['stats']
    }
</script>

<style scoped>
ul{
    list-style: none;
    margin:1rem;
    padding:0;
}

</style>