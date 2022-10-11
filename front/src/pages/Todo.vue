<template>
  <q-page class="bg-grey-3 column">
    <q-list class="list" separator bordered>
      <q-item v-for="(task, index) in tasks" :key="index" tag="label" v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary"/>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script setup>
import {reactive} from 'vue'

const tasks = reactive([
  {
    title: 'Open eyes',
    done:  false,
  },
  {
    title: 'Wake up',
    done:  false,
  },
  {
    title: 'Program',
    done:  false,
  },
])
</script>

<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'TodoPage',
})
</script>

<style lang="scss" scoped>
.list {
  background-color: $main-background;
}
</style>
