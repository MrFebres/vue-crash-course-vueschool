<script>
export default {
  props: {
    nombre: { String },
    url: { String }
  }
}
</script>

<template>
  <div>
    <img alt="nombre" src="url" />
    <h2>{{ nombre }}</h2>
    <a :href="url" target="_blank">Descargar</a>
  </div>
</template>

<style scoped>
a {
  background-color: #301675;
  border-radius: 5px;
  color: snow;
  padding: 0.3rem;
  text-decoration: none;
}

div {
  border-radius: 8px;
  border: 1px solid #f2f2f2;
  margin: 4px;
  padding: 1%;
  text-align: center;
}

img {
  padding: 0.5rem;
  width: 8rem;
}
</style>
