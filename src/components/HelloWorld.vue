<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li>
        <a
          href="https://developers.liveperson.com/agent-workspace-sdk-overview.html"
          target="_blank"
        >
          Agent Workspace SDK
        </a>
      </li>
      <li>
        <a
          href="https://developers.liveperson.com/guides-agent-workspace-widget.html"
          target="_blank"
        >
          How to add Custom Widget
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Custom Widget',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #FF7F00;
}
</style>
