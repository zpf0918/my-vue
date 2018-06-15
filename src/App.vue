<template>
  <div id="app"  class="container" >
    <div class="row justify-content-md-center">
      <TaskMenu v-on:click-select="onSelected" v-bind:items="menus"/>
      <TaskList v-bind:tag="currentMenuTag" v-bind:items="tasks" v-on:click-complete="onCompleted"/>
    </div>
  </div>
</template>

<script>
import TaskMenu from './components/TaskMenu.vue';
import TaskList from './components/TaskList.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    TaskMenu,
    TaskList,
  },
  data: function() {
    return {
      menus: [
        { tag: true,   text: '已完成'},
        { tag: false, text: '未完成'}
      ],
      currentMenuTag: false,
      tasks: function() {
        let tasks = [];
        for(let i = 0; i < 10; i++){
          tasks.push({
            id: i + 1,
            title: 'task' + (i + 1),
            content: 'content' + (i + 1),
            completed: false,
            createAt: (new Date()).toString()
          })
        }

        return tasks;
      }()
    }
  },
  beforeCreate() {
      axios.get('https://api.myjson.com/bins/khn66')
      .then(response => response.data)
      .then(data => (this.tasks = data))
      .catch(console.log);
  },
  methods: {
    onSelected(tag) {
      this.currentMenuTag = tag;
    },
    onCompleted(id) {
      this.tasks[id - 1].completed = true;
      this.save();
    },
    save() {
        axios.put('https://api.myjson.com/bins/khn66', this.tasks)
        .then(response => response.data)
        .then(data => alert('更新成功'))
        .catch(console.log);
      }
  }
}
</script>
