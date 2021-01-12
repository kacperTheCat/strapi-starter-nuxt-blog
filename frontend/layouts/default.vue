<template>
  <div class="main-wrapper">
    <nav class="uk-navbar-container" uk-navbar>
      <div class="uk-navbar-left">
        <ul class="uk-navbar-nav">
          <li>
            <a href="#modal-full" uk-toggle><span uk-icon="icon: table" /></a>
          </li>
          <li>
            <nuxt-link to="/" tag="a">Strapi Blog</nuxt-link>
          </li>
        </ul>
      </div>

      <div class="uk-navbar-right-custom">
        <ul class="uk-navbar-nav">
          <li v-for="(item, index) in menu" :key="index">
            <nuxt-link :to="item.path.slug" tag="a">
              {{ item.name }}
            </nuxt-link>
          </li>
        </ul>
      </div>
    </nav>

    <div id="modal-full" class="uk-modal-full" uk-modal>
      <div class="uk-modal-dialog">
        <button
          class="uk-modal-close-full uk-close-large"
          type="button"
          uk-close
        />
        <div
          class="uk-grid-collapse uk-child-width-1-2@s uk-flex-middle"
          uk-grid
        >
          <div
            class="uk-background-cover"
            style="
              background-image: url('https://images.unsplash.com/photo-1493612276216-ee3925520721?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=3308&q=80 3308w');
            "
            uk-height-viewport
          />
          <div class="uk-padding-large">
            <h1 style="font-family: Staatliches">Karolina Wojtkowska</h1>
            <div class="uk-width-1-2@s">
              <ul class="uk-nav-primary uk-nav-parent-icon" uk-nav>
                <li v-for="(item, index) in menu" :key="index">
                  <nuxt-link
                    class="uk-modal-close"
                    :to="item.path.slug"
                    tag="a"
                  >
                    {{ item.name }}
                  </nuxt-link>
                </li>
              </ul>
            </div>
            <p class="uk-text-light">Built with strapi</p>
          </div>
        </div>
      </div>
    </div>
    <nuxt />
  </div>
</template>

<script>
export default {
  async fetch() {
    this.categories = await this.$strapi.find("categories");
  },
  data: function () {
    return {
      categories: [],
      menu: [
        { name: "Strona główna", path: { slug: "/" } },
        { name: "O mnie", path: { slug: "/o-mnie" } },
        { name: "Blog", path: { slug: "/blog" } },
        { name: "Oferta", path: { slug: "/oferta" } },
        { name: "Kontakt", path: { slug: "/kontakt" } },
      ],
    };
  },
};
</script>

<style scoped>
body {
  background: red !important;
}

@media (max-width: 1000px) {
  .uk-navbar-container {
    display: flex;
    justify-content: flex-start;
  }

  .uk-navbar-right-custom {
    display: none;
    margin-left: 0 !important;
  }

  .uk-modal-dialog {
    min-height: 100vh;
  }

  .uk-background-cover.uk-first-column {
    display: none;
  }
}
</style>
