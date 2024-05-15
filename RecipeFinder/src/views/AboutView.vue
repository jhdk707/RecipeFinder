<template>
  <div class="about">
    <div class="contentbg relative items-center justify-center">
    <h1> Mission statement: The goal behind this project is to help reduce foodwaste, by providing a resource for users to make them most out of the ingredients that they have on hand before it goes bad, and reducing money spent on new ingredients. It is important to me to be able to use as much food as possible in as many different ways as possible before resorting to having to throw it out (or preferably compost if an option)</h1>
    <h1>This app was built as a project to have some fun combining two of my passions. Food & coding. Thanks to David at Spoonacular for building such a great API to play with and make this possible.</h1>
    <h2> Future developments will include: equipment needed, a "pro" account that allows you to login and save recipes, and more to come. If you think of anything let me know! </h2>
    <div class="donatecontainer">
  <p class="donateheader relative flex items-center justify-center">Want to support this free-to-use project?</p>
  <a href="https://venmo.com/u/tubeampmonolith" class="venmo-button" id="venmoLink">
    <img src="@/components/icons/venmo-logo.png" alt="Venmo Logo" class="venmo-logo">
  </a>
</div>
    <hr>
    <p class="footertext relative flex items-center justify-center">Built by Web Warlocks | 04-24-2024 | Built with Vuejs3</p>
    </div>
  </div>
</template>

<script>
document.addEventListener('DOMContentLoaded', function () {
  var venmoLink = document.getElementById('venmoLink');
  if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
    venmoLink.href = "venmo://u/tubeampmonolith"; // Venmo app URL
  }
});
</script>

<style scoped>

.about{
 display: block;
 margin: 5em;
 width: auto;
 overflow: hidden;
 align-items: center;
 position: fixed;
}

h1{
  text-align: left;
  margin-top: 1em;
}

h2{
  text-align: left;
  margin-top: 2em;
}

.footertext{
font-size: medium;
}

.contentbg{
  background: rgba(255,255,255,0.7);
  color: black;
  font-weight: 700;
  border-radius: 10px;
  padding: 20px;
}

.venmo-logo {
  height: 50px; /* Adjust the size as needed */
  width: auto;
}

.venmo-button {
  display: inline-block;
  background-color: #ffffff; 
  color: white;
  padding: 10px 10px;
  text-align: center;
  border-radius: 10px;
  text-decoration: none; 
  font-size: 16px;
  font-weight: bold;
  transition: background-color 0.3s ease;
  width: 25%;
}

.venmo-button:hover {
  background-color: #347ca5; 
}

.donatecontainer{
  display: flex;
  align-items: center; 
  justify-content: center; 
  background: rgba(156, 250, 162, 0.558);
  padding: 0.5em;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  margin: auto;
  width: 100%; 
  height: auto; 
  margin-bottom: 1em;
  margin-top: 1em;
}

.donateheader {
  margin-right: 3em;
}

@media (max-width: 680px) {
  .about {
    display: block;
    align-items: center;
    margin: 1em;
    overflow: hidden;
    position: fixed;
  }

  .venmo-button {
  display: block; /* Changed to inline-flex for better control of internal alignment */
  align-items: center; /* Center content vertically inside the button */
  justify-content: center; /* Center content horizontally inside the button */
  background-color: #ffffff; 
  padding: 10px 20px;
  border-radius: 10px;;
  transition: background-color 0.3s ease;
  width: 50%;
}

.venmo-button:hover {
  background-color: #347ca5; 
}

.donatecontainer {
  display: flex;
  align-items: center; 
  justify-content: center; 
  background: rgba(156, 250, 162, 0.558);
  padding: 0.5em;
  border-radius: 10px;
  color: rgb(0, 0, 0);
  margin: auto;
  width: 100%; 
  height: auto; 
  margin-bottom: 1em;
  margin-top: 1em;
}

.venmo-logo {
  height: 30px; 
  width: auto;
}

.footertext{
  margin-top:.25em;
  text-align: center;
}


}
</style>
