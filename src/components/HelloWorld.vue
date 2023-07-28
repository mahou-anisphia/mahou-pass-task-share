<template>
  <div class="hello">
    <h1>Welcome, {{ firstName }} {{ lastName }}!</h1>
    <p>What's your name?</p>
    <label for="fname"
      >First Name:<input name="fname" type="text" v-model="firstName"
    /></label>
    <br />
    <label for="lname"
      >Last Name:<input name="lname" type="text" v-model="lastName"
    /></label>
    <br />
    <input
      type="radio"
      id="mahou"
      name="scene"
      value="mahou"
      v-model="selectedOption"
    />
    <label for="mahou">Mahou</label>
    <input
      type="radio"
      id="nonMahou"
      name="scene"
      value="nonMahou"
      v-model="selectedOption"
    />
    <label for="nonMahou">Non - Mahou</label>

    <div class="container">
      <div class="row justify-content-center">
        <div
          v-if="selectedOption === 'mahou'"
          class="image-container col-sm-6 text-center"
        >
          <img src="imgs/mahou.png" alt="Mahou Image" class="img-fluid" />
        </div>
        <div
          v-else-if="selectedOption === 'nonMahou'"
          class="image-container col-sm-6 text-center"
        >
          <img
            src="imgs/non_mahou.png"
            alt="Non-Mahou Image"
            class="img-fluid"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    firstName: "Mahou",
    lastName: "user",
    selectedOption: "mahou",
  }),
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
[v-cloak] {
  display: none;
}
.img-fluid {
  max-height: 600px;
}
</style>
