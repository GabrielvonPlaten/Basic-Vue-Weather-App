<template>
  <div class="header">
    <nav>
      <div class="nav-wrapper green darken-2">
        <a href="localhost:3000" class="brand-logo center hide-on-small-and-down">Vue Weather App</a>
        <ul id="nav-mobile" class="right">
          <li>
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/forecast">Forecast</router-link>
          </li>
          <li>
            <router-link to="/about">About</router-link> 
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<style lang="scss">
  .header {
    text-align: center;
  }

  .header-list {
    padding: 0;
    margin: 0;
  }

  .header-list li {
    display: inline-block;
    margin: 0 10px;
    font-size: 1.2em;
  }
</style>
