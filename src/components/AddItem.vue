<template>
    <form action="" class="flex" @submit.prevent="addItem">
        <input type="text" v-model="newItem" class="text-black">
        <input type="submit" value="저장" class="px-3 py-2 border border-gray-500 ml-2">
    </form>
</template>

<script>
export default {
    data(){
        return {
            newItem: ''
        }
    },
    methods: {
        addItem(){
            if(this.newItem == ''){
                return alert('해야할 일을 입력하세요');
            }
            this.$emit('addItem', this.newItem);
            this.newItem = '';
        }
    }
}
</script>