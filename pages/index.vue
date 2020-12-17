<template>
  <div>
    <div class="intro">
      <img class="intro__bg" :src="intro.image" alt="">
      <div class="intro__container container">
        <div class="intro__box">
          <h1>{{ intro.title }}</h1>
          <h2>{{ intro.description }}</h2>
          <nuxt-content :document="intro" />
        </div>
      </div>
    </div>
    <div class="container">
      <h2>Blog</h2>
      <ul>
        <li v-for="post of posts" :key="post.slug">
          <NuxtLink :to="post.slug">
            {{ post.title }}
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content }) {
    const posts = await $content('blog').fetch()
    const intro = await $content('home/intro').fetch()

    return {
      intro,
      posts
    }
  },
  head () {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }]
    }
  }
}
</script>

<style>
.intro {
  position: relative;
  margin-bottom: 80px;
}

.intro__bg {
  position: absolute;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.intro__container {
  position: relative;
  z-index: 2;
  padding-top: 104px;
  padding-bottom: 104px;
}

.container {
  margin: 0 auto;
  width: 100%;
  max-width: 600px;
}
</style>
