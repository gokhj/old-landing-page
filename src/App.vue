<template>
  <div id="app">
    <v-divider></v-divider>
    <toggle-button
      @change="changeTheme()"
      :value="theme"
      :labels="{ checked: 'Dark Mode', unchecked: 'Light Mode' }"
      :color="{ checked: '#6e6e6e', unchecked: '#233646' }"
      :width="80"
      class="float-right sm:mr-10 lg:mr-24 xl:mr-40"
    />
    <div class="pb-20">
      <About second_occupation="Tea Lover" />
      <Contact />
    </div>
  </div>
</template>

<script>
  import About from "./components/About.vue";
  import Contact from "./components/Contact";

  export default {
    name: "App",
    components: {
      About,
      Contact,
    },
    data: function() {
      return {
        theme: localStorage.getItem("theme")
          ? JSON.parse(localStorage.theme)
          : true,
      };
    },
    methods: {
      changeTheme: function() {
        this.theme = !this.theme;
        this.changeProperties();
      },
      changeProperties: function() {
        document.body.classList.toggle("light-background");
        const items = ["name", "occupation", "body", "blog"];
        items.forEach((item) => {
          document.getElementById(item).classList.toggle("dark-text");
        });
      },
    },
    mounted() {
      if (localStorage.theme) {
        this.theme = JSON.parse(localStorage.theme);
        if (!this.theme) {
          this.changeProperties();
        }
      }
    },
    watch: {
      theme(newTheme) {
        localStorage.theme = newTheme;
      },
    },
  };
</script>

<style>
  @import "./assets/styles/tailwind.css";
  @import "./assets/styles/tufte.min.css";
  body {
    background-color: #233646;
  }
  .light-background {
    background-color: #ffffff;
  }
  .dark-text {
    color: #233646 !important;
  }
  .links {
    text-decoration: underline !important;
    background: unset !important;
    text-shadow: unset !important;
  }
</style>
