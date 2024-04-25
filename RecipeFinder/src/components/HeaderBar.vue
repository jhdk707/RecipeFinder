 <template>
    <div class="greetings">
        <div class="header-content">
      <img alt="Vue logo" class="logo" src="@/assets/Womanwithchicken.webp" width="200" height="200" />
      <div class="header-text">
        <h1>Welcome to Jesse's Recipe Finder</h1>
        <h3>Can't quite figure out what to make with what you have? Enter your ingredients, and we'll give you some ideas!</h3>
      </div>
    </div>
      <nav class="nav-bar flex items-center justify-between bg-gray-700 p-2">
        <div class="block lg:hidden">
      <button @click="toggleMobileMenu" class="text-white">
        &#9776; 
      </button>
    </div>
      <div :class="{'hidden': !mobileMenuOpen, 'flex': mobileMenuOpen}" class="flex-col lg:flex-row lg:flex">
      <router-link to="/" class="nav-item" @click="closeMenu">
        <a :class="{ 'router-link-exact-active': isActive('/') }" class="link">Home</a>
      </router-link>
      <router-link to="/about" class="nav-item" @click="closeMenu">
        <a :class="{ 'router-link-exact-active': isActive('/about') }" class="link">About</a>
      </router-link>
      <router-link to="/search" class="nav-item" @click="closeMenu">
        <a :class="{ 'router-link-exact-active': isActive('/search') }" class="link">Search</a>
      </router-link>
    </div>
    </nav>
    </div>
  </template>

  <script setup>
    import { useRoute } from 'vue-router';
    import { ref } from 'vue';

    const route = useRoute();
    const mobileMenuOpen = ref(false);

    const toggleMobileMenu = () => {
        mobileMenuOpen.value = !mobileMenuOpen.value;
    };
    const closeMenu = () => {
        mobileMenuOpen.value = false;
    };

    const isActive = (routePath) => {
  return route.path === routePath;
};
  </script>

  <style>

.header-content {
  display: flex;
  align-items: center; /* Aligns items vertically in the center */
  justify-content: start; /* Aligns items horizontally to the start */
}

.header-text {
  margin-left: 20px; /* Adds space between the image and the text */
}

.nav-bar {
  background-color: gray;
  padding: 1rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>

<style scoped>
.greetings h1 {
  color: green; /* Moved inline style to CSS */
}

.nav-item {
  padding: 10px;
  color: white;
  text-decoration: none;
}

@media (max-width: 768px) { /* Example breakpoint for mobile devices */
  .nav-item {
    display: block;
    width: 100%;
  }
}
</style>