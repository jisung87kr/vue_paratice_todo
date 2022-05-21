<template>
    <li>
        <input type="button" :value="tag"
        class="border border-gray-700 py-1 px-2 text-[10px] rounded-md"
        :class="{'border-indigo-500 text-indigo-500' : active}"
        @click="setCurrentTag"
        >
    </li>
</template>

<script>
export default {
    props: {
        tag: String,
        active : Boolean
    },
    data(){
        return{
            tagName: this.tag
        }
    },
    methods: {
        setCurrentTag(){
            console.log(this.tagName);
            this.$emit('updateCurrentTag', this.tagName);
        }
    }
}
</script>