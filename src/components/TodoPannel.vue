<template>
    <div 
        :class="{
            'bg-gray-800 text-white' : theme == 'dark',
            'bg-gray-100 text-black' : theme == 'light',
            }"
    >
        <slot></slot>
    </div>
</template>
<script>
export default {
    props: {
        theme: String
    }
}
</script>