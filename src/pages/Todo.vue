<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      Add task
    </div>
    <q-list
      class="bg-white"
      separator
      bordered>
      <q-item
        clickable
        v-for="(task,index) in tasks"
        key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1' : task.done}"
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section
        v-if="task.done"
        side>
          <q-btn
            @click.stop="deleteTask(index)"
            flat
            round
            color="red"
            icon="delete"
          />
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
export default {
 data(){
   return {
     tasks: [
       {
         title: 'Estudar Laravel',
         done: false
       },
       {
         title: 'Estudar Vue JS',
         done: false
       },
       {
         title: 'Estudar Tests',
         done: false
       }
     ]
   }
 },
  methods: {
    deleteTask(index){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to delete the task?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task Deleted!')
      })
    }
  }
}
</script>

<style lang="scss">
  .done{
    .q-item__label {
      text-decoration: line-through;
      color:#bbb;
    }
  }
</style>
