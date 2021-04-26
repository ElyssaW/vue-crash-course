<template>
    <div :class="[task.reminder ? 'reminder' : '']">
        <h4>Task 
            <i @click="onDelete(task.id)" class="fas fa-times"></i>
        </h4>
        <h5>{{task.text}} for {{task.day}}</h5>
        <p>Toggle reminder: <i @click="toggleReminder(task.id)" class="fas fa-times"></i></p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    },
    methods: {
        onDelete(taskId) {
            console.log(taskId)
            this.$emit('delete-task', taskId)
        },
        toggleReminder(taskId) {
            console.log('Toggling reminder')
            this.$emit('toggle-reminder', taskId)
        }
    }
}
</script>

<style scoped>
    .fas{
        color: red;
    }

    .reminder {
        border-left: solid 5px green;
    }
</style>