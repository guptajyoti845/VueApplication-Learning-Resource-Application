<template>
  <ul>
    <learning-resource v-for='res in resources' :key='res.id' :description='res.description'
                       :id='res.id'
                       :title='res.title' :link='res.link'></learning-resource>
  </ul>
</template>

<script>
import LearningResource from '@/components/LearningResources/LearningResource';

export default {
  name: 'StoredResources',
  inject: ['resources'],
  components: {
    LearningResource
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
