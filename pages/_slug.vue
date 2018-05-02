<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-offset-2 is-8">
          <p class="subtitle is-6">
            <nuxt-link to="/">Back to Blog home</nuxt-link>
          </p>
          <h1 class="title is-2">
            {{ stadium.fields.name }}
          </h1>
          <table class="table">
            <tbody>
            <tr v-for="(field, key) in stadium.fields" :key="key">
              <td><strong>{{ key }}</strong></td>
              <td>{{ field }}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import client from '~/plugins/contentful';

export default {
  asyncData({ params, error, payload }) {
    if (payload) return { stadium: payload };

    return client
      .getEntries({
        content_type: 'stadium',
        'fields.slug': params.slug,
      })
      .then(entries => {
        return { stadium: entries.items[0] };
      })
      .catch(e => console.log(e));
  },
  head() {
    return {
      title: this.stadium.fields.name,
    };
  },
};
</script>
