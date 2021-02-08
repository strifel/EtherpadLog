<template>
  <h2 class="title is-2" style="width: 100%">
    Bitte wählen Sie eine Etherpad Datei aus
  </h2>
  <input type="file" v-bind="data" accept=".etherpad" @change="upload">
</template>

<script>
import { Options, Vue } from 'vue-class-component';

@Options({
  data() {
    return {
      data: null,
    };
  },
  methods: {
    /* eslint-disable */
    upload: function (event) {
      const file = event.target.files[0];
      const reader = new FileReader();
      reader.onload = (function() {
        return function(e) {
          this.$emit('input', JSON.parse(e.target.result));
        };
      })(file).bind(this);
      reader.readAsText(file);
    },
    /* eslint-enable */
  },
})

export default class NavBar extends Vue {}

</script>

<style scoped>

</style>
