<template>
  <div class="home">
    <BlogPost v-if="!user" :post="welcomeScreen" />
    <BlogPost :post="post" v-for="(post, index) in blogPostsFeed" :key="index" />
    <div class="blog-card-wrap">
      <div class="container">
        <h3>View More Recent Blogs</h3>
        <div class="blog-cards">
          <BlogCard :post="post" v-for="(post, index) in blogPostsCards" :key="index" />
        </div>
      </div>
    </div>
    <div class="chart">
      <Chart />
    </div>
    <div v-if="!user" class="updates">
      <div class="container">
        <h2>Never miss a post. Register for your free account today!</h2>
        <router-link class="router-button" :to="{ name: 'Login' }">
          Register for EZ Trading <Arrow class="arrow arrow-light" />
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import BlogPost from "../components/BlogPost";
import BlogCard from "../components/BlogCard";
import Arrow from "../assets/Icons/arrow-right-light.svg";
import Chart from '../components/Chart'

export default {
  name: "Home",
  components: { BlogPost, BlogCard, Arrow, Chart },
  data() {
    return {
      welcomeScreen: {
        title: "Welcome!",
        blogPost:
        "Weekly blog articles with all things investing including trading strategies, market analysis, stock news and more. Register today to never miss a post!",
        welcomeScreen: true,
        photo: "investing",
      },
    };
  },
  computed: {
    blogPostsFeed() {
      return this.$store.getters.blogPostsFeed;
    },
    blogPostsCards() {
      return this.$store.getters.blogPostsCards;
    },
        user() {
          return this.$store.state.user;
        },
  },
};
</script>

<style lang="scss" scoped>

.blog-card-wrap {
  h3 {
    font-weight: 300;
    font-size: 28px;
    margin-bottom: 32px;
  }
}

.chart {
  height: 500px;
  bottom: 5rem;
  padding-bottom: 5rem;

  @media(min-width: 800px) {
    height: 850px;
    padding-top: 8rem;
    padding-left: 5rem;
    padding-right: 5rem;
    padding-bottom: 5rem;
  }
}

.updates {
  .container {
    padding: 100px 25px;
    display: flex;
    flex-direction: column;
    align-items: center;
    @media (min-width: 800px) {
      padding: 125px 25px;
      flex-direction: row;
    }

    .router-button {
      display: flex;
      font-size: 14px;
      text-decoration: none;
      height: 41.5px;

      @media(min-width: 800px) {
        margin-left: auto;
      }
    }

    h2 {
      font-weight: 300;
      font-size: 32px;
      max-width: 425px;
      width: 100%;
      text-align: center;
      text-transform: uppercase;
      @media(min-width: 800px) {
        text-align: initial;
        font-size: 40px;
      }
    }
  }
}
</style>
