<template>
	<Layout>
		<!-- Page Header -->
    <header class="masthead" :style="{ backgroundImage: 'url(/img/home-bg.jpg)' }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1># {{ $page.tag.title }}</h1>
              <span class="subheading">A Blog Theme by Start Bootstrap</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <template v-for="post of $page.tag.posts">
            <div :key="post.id" class="post-preview">
              <g-link :to="'/post/' + post.id">
                <h2 class="post-title">
                  {{ post.title }}
                </h2>
              </g-link>
            </div>
            <hr :key="post.id + 'hr'" />
          </template>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
	query ($id: ID!) {
		tag: strapiTag (id: $id) {
			id
			title
			posts {
				id
				title
			}
		}
	}
</page-query>

<script>
	export default {
		name: 'TagPage'
	}
</script>

<style lang="scss" scoped>

</style>