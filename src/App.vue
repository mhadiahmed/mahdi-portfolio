<template>
  <transition name="fade" tag="div" class="wrapper" mode="out-in">
    <div class="wrapper" v-if="isLoaded" id="app">
      <LandingPage :user="user" />
      <Description
        :user="user"
        :content="findSlug('description')"
        :links="findSlug('links')"
      />
      <Experience :content="findSlug('experiences')" />
      <Skills :content="findSlug('skills')" />
      <Projects :content="findSlug('projects')" />
      <Achievement :content="findSlug('achievement')" />
      <Footer :user="user" :links="findSlug('links')" />
    </div>
  </transition>
</template>

<script>
import LandingPage from "./components/LandingPage.vue";
import Description from "./components/Description.vue";
import Experience from "./components/Experience.vue";
import Skills from "./components/Skills.vue";
import Projects from "./components/Projects.vue";
import Footer from "./components/Footer.vue";
import Achievement from "./components/Achievement.vue";
import mahdi from "../data/mahdi.json";

export default {
  name: "App",
  components: {
    LandingPage,
    Description,
    Experience,
    Skills,
    Achievement,
    Projects,
    Footer,
  },
  data() {
    return {
      isLoaded: false,
      user: null,
      posts: mahdi,
    };
  },
  methods: {
    findSlug(slug) {
      let post;
      this.posts.data.map((item) => {
        if (item.slug === slug) {
          post = item;
        }
      });
      return post;
    },
    getUser() {
      let user_data;
      mahdi.data.map((item) => {
        if (item.slug === "user-data") {
          user_data = item;
        }
      });
      return user_data;
    },
  },

  mounted() {
    document.body.classList.add("loading");
    let user_data = this.getUser();
    this.user = {
      name: user_data.metdata.name,
      status: user_data.metdata.status,
      email: user_data.metdata.email,
      phone: user_data.metdata.phone,
      city: user_data.metdata.city,
      lang: user_data.metdata.lang,
      photo: user_data.metdata.photo,
    };
    this.isLoaded = true;
    this.$nextTick(() => document.body.classList.remove("loading"));
    console.log(this.user);
  },
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

#app {
  font-family: Montserrat-Regular, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.wrapper {
  height: 100%;
}
</style>
