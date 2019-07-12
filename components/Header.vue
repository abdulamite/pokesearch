<template>
  <div>
      <header>
            <img src="http://pngimg.com/uploads/pokeball/pokeball_PNG21.png" alt="logo">
            <h1>Pokésearch</h1>
        </header>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    width: 100%;
}

header{
    display: flex;
    text-align: left;
    max-height: 20vh;
    background-color:#003A70;
    margin: 0;
    padding: .3rem;
    color:white;
    font-family: 'Oswald', sans-serif;
}

header>img{
    height: 50px;
    width: 50px;
    margin-right: .5rem;
}

</style>