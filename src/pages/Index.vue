<template>
  <Layout>

    <!-- Page Header -->
    <header class="masthead" :style="{ backgroundImage: 'url('+ GRIDSOME_IMG_URL + general.cover.url +')' }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <template v-for="edge of $page.posts.edges">
            <div :key="edge.node.id" class="post-preview">
              <g-link :to="'/post/' + edge.node.id">
                <h2 class="post-title">
                  {{ edge.node.title }}
                </h2>
              </g-link>
              <h3 class="post-subtitle">
                <g-link :to="'/tag/' + tag.id" v-for="tag of edge.node.tags" :key="tag.id">{{ tag.title }} </g-link>
              </h3>
              <p class="post-meta">
                Posted by
                <a href="#">{{ edge.node.create_by.username }}</a>
                {{ edge.node.created_at }}
              </p>
            </div>
            <hr :key="edge.node.id + 'hr'" />
          </template>
          <pager :info="$page.posts.pageInfo"/>
        </div>
      </div>
    </div>

  </Layout>
</template>

<page-query>
  query ($page: Int) {
    posts: allStrapiPost (perPage: 2, page: $page) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          create_by {
            username
          }
          tags {
            id
            title
          }
          created_at
        }
      }
    }
    general: allStrapiGeneral {
      edges {
        node {
          id
          title
          subtitle
          cover {
            url
          }
        }
      }
    }
  }
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  name: 'HomePage',
  components: { Pager },
  metaInfo: {
    title: "Hello, world!",
  },
  computed: {
    general () {
      return this.$page.general.edges[0].node
    }
  }
};
</script>

<style>

</style>
