<template>
    <li class="border-b border-gray-700 first:border-t last:border-b-0 py-2 px-3 flex items-center justify-between">
        <label for="">{{ item.title }}</label>
        <input type="checkbox" class="ml-2" :checked="completed" @click="complete($event)">
    </li>
</template>
<script>
export default {
    props: {
        item: Object
    },
    data(){
        return{
            completed: this.item.completed
        }
    },
    methods: {
        complete(event){
            var item = {
                ...this.item,
                completed: event.target.checked,
            };
            this.$parent.$emit('complete', item);
        }
    }
}
</script>