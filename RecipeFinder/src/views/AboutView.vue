<template>
  <div class="about">
    <div class="contentbg">
    <h1>This app was built as a project to have some fun combining two of my passions. Food & coding. Thanks to David at Spoonacular for building such a great API to play with and make this possible.</h1>
    <h2> Future developments will include: equipment needed, a "pro" account that allows you to login and save recipes, and more to come. If you think of anything let me know! </h2>
    <div class="donatecontainer">
  <p class="donateheader">Want to support this project?</p>
  <a href="https://venmo.com/u/tubeampmonolith" class="venmo-button" id="venmoLink">
    <img src="@/components/icons/venmo-logo.png" alt="Venmo Logo" class="venmo-logo">
  </a>
</div>
    <hr>
    <p class="footertext">Built by Jesse Hudak 04-24-2024 | Built with Vuejs3</p>
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
 margin: 1em;
 width: auto;
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
font-size: small;
}

.contentbg{
  background: rgba(255,255,255,0.7);
  color: black;
  font-weight: 700;
  border-radius: 10px;
  padding: 10px;
}

.venmo-logo {
  height: 50px; /* Adjust the size as needed */
  width: auto;
}

.venmo-button {
  display: inline-block;
  background-color: #888b8e; 
  color: white;
  padding: 10px 10px;
  text-align: center;
  border-radius: 10px;
  text-decoration: none; 
  font-size: 16px;
  font-weight: bold;
  transition: background-color 0.3s ease;
  width: 100%;
}

.venmo-button:hover {
  background-color: #347ca5; 
}

.donatecontainer{
  background: rgba(156, 250, 162, 0.558);
  padding: .5em;
  border-radius: 10px;
  margin-top: .5em;
  margin-bottom: .5em;
}

@media (max-width: 680px) {
  .about {
    display: block;
    align-items: center;
    margin: 1em;
    overflow: hidden;
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
