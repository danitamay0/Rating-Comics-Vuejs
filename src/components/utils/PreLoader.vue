<template>
    <div class="text-center">
        <h2>{{label}}</h2>
        <img src="@/assets/loading.gif" />
    </div>
</template>

<script>
export default {
    name: 'PreLoader',
    props: {
        label: String
    }
}
</script>

<style scoped>
img {
    border-radius: 10px;
}
</style>
