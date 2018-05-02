<template>
  <div id="app">
    <ContentList :contentList="pclist"
      @textAdded="onTextAdded"
      @textRemoved="onTextRemoved"/>
  </div>
</template>

<script>
import ContentList from './components/ContentList';

const PREDEFINED_CONTENT_NS = 'le_pc';

export default {
  name: 'App',
  data() {
    return {
      pclist: [],
    };
  },
  components: {
    ContentList,
  },
  methods: {
    onTextAdded(text) {
      if (text.id) {
        localStorage.setItem(`${PREDEFINED_CONTENT_NS}_${text.id}`, text.text);
      }
    },
    onTextRemoved(id) {
      if (id) {
        localStorage.removeItem(`${PREDEFINED_CONTENT_NS}_${id}`);
      }
    },
  },
  created() {
    Object.keys(localStorage).forEach((key) => {
      if (key.indexOf(PREDEFINED_CONTENT_NS) === 0) {
        const text = { id: key.slice(PREDEFINED_CONTENT_NS.length + 1), text: localStorage[key] };
        this.pclist.push(text);
      }
    });
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
