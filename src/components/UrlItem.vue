<template>
  <li>
    <span>{{url.id}}</span> - <span>{{url.name}}</span> - <a :href="url.longUrl" target="_blank">{{url.longUrl}}</a>
    <button @click="handleEdit(url)" style="margin-left: 10px;">Edit</button>
  </li>
</template>

<script>
export default {
  name: 'url-item',
  props: {
    url: {
      type: Object,
      required: true
    }
  },
  methods: {
    handleEdit () {
      this.$emit('edit', this.url)
    }
  }
}
</script>


<style scoped>
a {
  color: red;
}
</style>