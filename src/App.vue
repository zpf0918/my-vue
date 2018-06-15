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
  methods: {
    onSelected(tag) {
      this.currentMenuTag = tag;
      },
    onCompleted(id) {
      this.tasks[id - 1].completed = true;
    }
  }
}
</script>
