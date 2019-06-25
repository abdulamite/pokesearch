<template>
  <div class="container">
    <Header />
    <div>
      <Form id="form"/>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Form from '~/components/Form.vue'
import Header from '~/components/Header.vue'

export default {
  components: {
    Logo,
    Form,
    Header
  }
}
</script>

<style>
.container {
  flex-direction: column;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

#form{
  margin-top:5rem;
}


.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
