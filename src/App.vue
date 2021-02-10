<template>
  <section class="main">
    <NavBar />
    <Upload v-if="!data" ref="upload" @input="dataUpload"/>
    <div v-else>
      <div v-for="message in data" :key="JSON.stringify(message)">
        <i>{{ message.author }}: </i><p>{{ message.text }}</p>
      </div>
    </div>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>EtherpadLog</strong> by <a href="https://strifel.de">Strifel</a>. The source code is licensed
          <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. Source can be found on <a href="https://github.com/strifel/EtherpadLog">Github</a>.
        </p>
      </div>
    </footer>
  </section>
</template>

<script lang="ts">
/* eslint-disable */
import { Options, Vue } from 'vue-class-component';
import 'bulma';

import NavBar from '@/components/NavBar.vue';
import Upload from '@/components/Upload.vue';

@Options({
  components: {
    NavBar,
    Upload,
  },
  data() {
    return {
      data: null,
    };
  },
  methods: {
    dataUpload: function (data: any) {
      let newData = [];
      for (let element in data) {
        console.log(element);
        if (element.includes("revs")) {
          let author = data['globalAuthor:' + data[element].meta.author];
          newData.push({'author': author ? author.name : 'unknown', 'text': data[element].changeset.replace(/^Z:.*\$/i, "")});
        }
      }
      this.data = newData;
    }
  }
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 20px;
}
</style>
