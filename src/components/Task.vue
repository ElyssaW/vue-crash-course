<template>
    <h4>Task</h4>
    <h5>{{task.text}} for {{task.day}}</h5>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    }
}
</script>
