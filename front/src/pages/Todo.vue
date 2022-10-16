<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
          v-model="newTask"
          class="col"
          filled square
          placeholder="Add task"
          bg-color="white"
          dense
          @keyup.enter="addTask"
      >
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addTask" />
        </template>
      </q-input>
    </div>

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
        </q-item-section>
      </q-item>
    </q-list>

    <div v-if="tasks.length === 0" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary"/>
      <div class="text-h5 text-center text-primary">
        No tasks
      </div>
    </div>
  </q-page>
</template>

<script setup>
import {ref, reactive} from 'vue'

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

const newTask = ref('')
const addTask = () => {
  tasks.push({
    title: newTask.value,
    done: false,
  })
  newTask.value = ''
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

.no-tasks {
  opacity: 0.5;
}
</style>
