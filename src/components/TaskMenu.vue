<template>
  <div class="col-md-1 mt-5">
    <div class="btn-group-vertical" role="group" v-for="item in items">
      <button type="button" class="btn btn-secondary" v-on:click="onSelected(item.tag)">{{ item.text }}</button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TaskMenu',
    props: {
      items: Array
    },
    methods: {
      onSelected(tag) {
        this.$emit('click-select', tag);
      }
    }
  }
</script>
