<template>
<div class="home">    
    

    <list-tasks
    v-if="$store.state.tasks.length"  
    />
    <no-tasks
    v-else/>
        <button-done-sorting />

    </div>
</template>

<script>
import ButtonDoneSorting from '@/components/Todo/ButtonDoneSorting.vue'

export default {
    name: 'Home',
    data() {
        return{ 
        }
    },
    methods: {
    },
    components: {
        'list-tasks' : require('@/components/Todo/ListTask.vue').default,
        'no-tasks' : require('@/components/Todo/NoTasks.vue').default,
        'button-done-sorting' : require('@/components/Todo/ButtonDoneSorting.vue').default
     }

}
</script>
