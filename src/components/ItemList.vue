<template>
    <div class="border w-1/6">
        <div class="py-2 px-3">
            <h1 class="font-bold mb-2"><slot/></h1>
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
        </div>
</template>
<script>
import TodoItem from './TodoItem'
import TodoTag from './TodoTag'

export default {
    components : {
        TodoItem,
        TodoTag
    },
    props: {
        todolist: Array
    },
    data(){
        return{
            currentTag: '전체',
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