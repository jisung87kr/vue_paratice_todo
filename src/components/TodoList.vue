<template>
    <div class="grid justify-items-center content-center h-screen bg-gray-900 gap-5">
        <ItemList 
            v-if="unCompletedList.length" 
            :todolist="unCompletedList" 
            @complete="complete"
        >
            <template #title>
                해야할 일
            </template>

            <template #addItem>
                <AddItem @addItem="addItem"></AddItem>
            </template>
        </ItemList>
        <ItemList 
            v-if="completedList.length" 
            :todolist="completedList" 
            @complete="complete"
            class="bg-gray-800 text-white"
        >
            완료한 일
        </ItemList>
    </div>
</template>
<script>
import ItemList from './ItemList'
import AddItem from './AddItem.vue'
export default {
    components: { 
        ItemList,
        AddItem,
    },
    data: function(){
        return {
            todolist: [
                { title: '터미널 가기', completed: false, id: 1, tag: '일상' },
                { title: '미용실 가기', completed: false, id: 2, tag: '일상'},
                { title: '뷰 학습 하기', completed: false, id: 3, tag: '자기개발' }
            ]
        }
    },
    computed: {
        completedList(){
            return this.todolist.filter(a => a.completed == true);
        },
        unCompletedList(){
            return this.todolist.filter(a => a.completed == false);
        },
    },
    methods: {
        complete(item){
            this.todolist.map(a => {
                if(a.id == item.id){
                    a.completed = item.completed
                }
            });
        },
        addItem(title){
            let data = {
                title : title,
                completed: false,
                id : this.todolist.length + 1,
                tag: '미분류'
            }
            this.todolist.push(data);
        }
    }
}
</script>