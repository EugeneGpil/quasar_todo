<template>
  <q-page class="bg-grey-3 column">
    <q-list class="list" separator bordered>
      <q-item
          v-for="(task, index) in tasks"
          :key="index"
          :class="{'done bg-blue-1': task.done}"
          tag="label"
          v-ripple
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary"/>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
              icon="delete"
              flat
              round
              dense
              size="sm"
              color="primary"
              @click="removeTask(index)"
          />
          <!--          @click="tasks = [...tasks.filter((_, taskIndex) => index !== taskIndex)]"-->
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

import {useQuasar} from 'quasar'

const $q = useQuasar()

const removeTask = (index) => {
  $q
      .dialog({
        title:      'Delete',
        message:    'Delete task?',
        cancel:     true,
        persistent: true,
      })
      .onOk(() => {
        tasks.splice(index, 1)
        $q.notify({
          message:  'Task was deleted',
          color:    'primary',
          position: 'bottom-right',
        })
      })
}
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

.done {
  .q-item {
    &__label {
      text-decoration: line-through;
      color: $text-secondary;
    }
  }
}
</style>
