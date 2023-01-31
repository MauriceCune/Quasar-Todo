<template>
  <q-page class="bg-grey-2 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        @keyup.enter="AddTask"
        class="col"
        bg-color="white"
        square
        filled
        placeholder="Add Task"
        dense>
        <template v-slot:append>
          <q-btn
            @click="AddTask"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white"
      separator
      bordered>
      <q-item
       v-for="(task, index) in tasks"
       :key="task.title"
       @click="task.done= !task.done"
       :class="{'done bg-blue-1': task.done}"
       clickable
        v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            val="teal"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>

        <q-item-section
        v-if="task.done"
        side>
        <q-btn
        @click.stop="deleteTask(index)"
          flat
          round
          dense
          color="primary" icon="delete" />
        </q-item-section>

      </q-item>

    </q-list>

    <div
      v-if="!tasks.length"
      class="no-Tasks absolute-center"
      >
      <q-icon
        name="check"
        size="100px"
        color="primary"
      />
      <div class="text-h5 text-primary text-center">
        No Tasks
      </div>
    </div>
  </q-page>
</template>

<script>
import { text } from 'body-parser'

export default {
  data () {
    return{

        newTask: '',
      tasks: [
      // {
      //   title: 'Get Bananas',
      //    done: false
      //  },
      //  {
      // title: 'Eat Bananas',
      //   done: false
      //  },
      //  {
      //    title: 'Poo Bananas',
      //  done: false
      // }
        ]
      }
    },
    methods: {
      deleteTask(index){
        this.$q.dialog({
        title: 'Confirm',
        message: 'Deseja eliminar permanentemente?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Tarefa eliminada')
      })

      },
      AddTask () {
        this.tasks.push({
          title:this.newTask,
          done:false
        })
        this.newTask=''
      }
    }
  }
</script>

<style lang="scss">
  .done{
    .q-item__label{
      text-decoration: line-through;
      color: rgb(224, 188, 188);
    }
  }

  .no-Tasks{
    opacity: 0.5;
  }
</style>
