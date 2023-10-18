<template lang="">
    <div>
        <button @click="arrDate.push(new Date().toLocaleTimeString())">Додати час натискання</button>
    <p>{{ arrDate }}</p>
    </div>
</template>
<script>
export default {
    data() {
        return {
            arrDate: [],
        }
    },
}
</script>
<style lang="">
    
</style>