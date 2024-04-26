<template>
  <div class="about">
    <h1>This app was built as a project to have some fun combining two of my passions. Food & coding. Thanks to David at Spoonacular for building such a great API to play with and make this possible.</h1>
    <p> Future developments will include: equipment needed, a "pro" account that allows you to login and save recipes, and more to come. If you think of anything let me know! </p>
    <p>Built by Jesse Hudak 04-24-2024 | Built with Vuejs3</p>
  </div>
</template>

<style scoped>

.about{
 display: block;
 padding: 1em;
 margin-left: 3em;
 margin-right: 3em;

}

h1{
  text-align: left;
  margin-top: 1em;
}

p{
  text-align: left;
  margin-top: 4em;
}

@media (max-width: 680px) {
  .about {
    display: block;
    align-items: center;
    margin: 5em;
    overflow: hidden;
  }
}
</style>
