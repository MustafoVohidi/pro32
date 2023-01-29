<template>
    <button @click="chooseColor" :style="{ background: color}" class="select_color">
    </button>
</template>
<script setup>
const props = defineProps({
color:String,
})
const emit=defineEmits([
'choose'
])
let chooseColor=()=>{
    emit("choose", props.color)
}
</script>
<style lang="scss">
    .select_color{
        display: inline-block;
        width: 20px;
        height: 20px;
        cursor: pointer;
    }
</style>