<template>
  <div class="pc-list">
    <input class="pc-list-input" v-model="newText"/>
    <div @click="addText" class="pc-list-add">Add</div>
    <ul>
      <li class="pc-list-item" v-for="item in combindList" :key="item.id">
        <div class="pc-list-item-text" @click="sendText(item.text)">{{ item.text }}</div>
        <div class="pc-list-item-remove" @click="removeText(item.id)">X</div>
      </li>
    </ul>
  </div>
</template>

<script>
import agentSDK from '../agentSDK';

export default {
  name: 'ContentList',
  props: {
    contentList: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      newText: '',
      localList: [],
    };
  },
  computed: {
    combindList() {
      return this.contentList.concat(this.localList);
    },
  },
  methods: {
    sendText: (text) => {
      const cmdName = agentSDK.cmdNames.write;
      const data = { text };

      agentSDK.command(cmdName, data);
    },
    addText() {
      if (this.newText) {
        const text = { id: new Date().getTime(), text: this.newText };
        this.$set(this.localList, this.localList.length, text);
        this.$emit('textAdded', text);
        this.newText = '';
      }
    },
    removeText(id) {
      if (id) {
        let idx = this.contentList.findIndex(item => item.id === id);
        let emitEvent = false;
        if (idx > -1) {
          this.contentList.splice(idx, 1);
          emitEvent = true;
        } else {
          idx = this.localList.findIndex(item => item.id === id);
          if (idx > -1) {
            this.localList.splice(idx, 1);
            emitEvent = true;
          }
        }
        if (emitEvent) {
          this.$emit('textRemoved', id);
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.pc-list {

  .pc-list-input {
    float: left;
    height: 28px;
    width: calc(100% - 46px);
  }

  .pc-list-add {
    float: right;
    border: solid 1px #767678;
    padding: 5px;
    margin-right: -2px;
    width: 30px;
    cursor:pointer;

    &:hover {
      background: #d6d6d6;
    }
  }

  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
  }
  .pc-list-item {
    width: 100%;
    border: solid 1px #767678;
    margin-top: -1px;
    line-height: 40px;
    position: relative;

    &:hover {
      background: #d6d6d6;
    }

    .pc-list-item-text {
      cursor:pointer;
      color:blue;
      text-decoration:underline;
    }

    .pc-list-item-remove {
      position: absolute;
      top: 4px;
      right: 6px;
      border: solid 1px #767678;
      border-radius: 30px;
      width: 30px;
      line-height: 30px;
      font-weight: bold;
      background: #fff;
      cursor:pointer;
    }
  }
}
</style>
