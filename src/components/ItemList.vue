<template>
    <TodoPannel 
    class="border border-gray-700 w-1/6"
    :theme="theme"
    >
        <div class="py-2 px-3">
            <h1 class="font-bold mb-2"><slot name="title"/></h1>
            <ul class="flex gap-1">
                <TodoTag v-for=" (tag, index) in tags" 
                    :key="index" 
                    :tag="tag"
                    :active="tag == currentTag"
                    @updateCurrentTag="updateCurrentTag"
                >
                </TodoTag>
            </ul>
        </div>
        <ul>
            <TodoItem v-for="item in filter" 
                :key="item.id" 
                :item="item"
             >
             </TodoItem>
        </ul>
        <slot name="addItem"></slot>
    </TodoPannel>
</template>
<script>
import TodoItem from './TodoItem'
import TodoTag from './TodoTag'
import TodoPannel from './TodoPannel.vue'

export default {
    components : {
        TodoItem,
        TodoTag,
        TodoPannel
    },
    props: {
        todolist: Array
    },
    data(){
        return{
            currentTag: '전체',
            theme: 'dark',
        }
    },
    computed: {
        tags(){
            return ['전체', ...new Set(this.todolist.map(a => a.tag))];
        },
        filter(){
            if(this.currentTag == '전체'){
                return this.todolist;
            }
            return this.todolist.filter(a => a.tag == this.currentTag);
        }
    },
    methods: {
        updateCurrentTag(tag){
            this.currentTag = tag;
        }
    }
}
</script>