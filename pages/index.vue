<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-offset-2 is-8">
          <h1 class="title is-2">All Stadiums</h1>
          <hr>

          <h2
            class="title is-4"
            v-for="(stadium, index) in stadiums"
              :key="index">
            <nuxt-link :to="stadium.fields.slug">
              {{ stadium.fields.name }}
            </nuxt-link>
          </h2>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import client from '~/plugins/contentful';

export default {
  asyncData({ params }) {
    return client
      .getEntries({
        content_type: 'stadium',
        // order: '-sys.createdAt',
      })
      .then(entries => {
        return { stadiums: entries.items };
      })
      .catch(e => console.log(e));
  },
  head: {
    title: 'All Stadiums',
  },
};
</script>

