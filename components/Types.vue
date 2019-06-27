<template>
    <div class="types">
        <p v-for="type in types" :class="type.type.name"> {{ (type.type.name).toUpperCase() }} </p>
    </div>
</template>

<script>
    export default {
        props:['types']
    }
</script>

<style scoped>

.types{
    display: flex;
    justify-content: center;
    margin:.5rem;
}

.types>p{
    margin:.3rem;
    padding:.5rem;
    border-radius: .2rem;
}

.rock{
    background-color:#bcaaa4;
}

.ground{
    background-color:#a1887f;
}

.electric{
    background-color:#fff176;
}

.grass{
    background-color:#aed581;
}

.ghost{
    background-color:#b0bec5;
}

.poison{
    background-color:#ba68c8;
}

.steel{
    background-color:#e0e0e0;
}
.fighting{
    background-color: #ef5350;
}
.fire{
    background-color:#ff7043;
}
.flying{
    background-color:#f3e5f5;
}
.psychic{
    background-color:#ce93d8;
}
.ice{
    background-color:#29b6f6;
}
.bug{
    background-color:#aed581;
}
.dragon{
    background-color:#b559dc;
}
.dark{
    background-color:#78909c;
}
.fairy{
    background-color:#f06292;
}
.water{
    background-color:#82afe9;
}
.normal{
    background-color:#c5bebe;
}




</style>