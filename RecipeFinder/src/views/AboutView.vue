<template>
  <div class="about">
    <div class="contentbg">
    <h1>This app was built as a project to have some fun combining two of my passions. Food & coding. Thanks to David at Spoonacular for building such a great API to play with and make this possible.</h1>
    <p> Future developments will include: equipment needed, a "pro" account that allows you to login and save recipes, and more to come. If you think of anything let me know! </p>
    <p>Built by Jesse Hudak 04-24-2024 | Built with Vuejs3</p>
    </div>
  </div>
</template>

<style scoped>

.about{
 display: block;
 padding: 1em;
 margin-left: 2em;
 margin-right: 2em;

}

h1{
  text-align: left;
  margin-top: 1em;
}

p{
  text-align: left;
  margin-top: 4em;
}

.contentbg{
  background: rgba(255,255,255,0.7);
  color: black;
  font-weight: 700;
  border-radius: 10px;
  padding: 10px;
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
