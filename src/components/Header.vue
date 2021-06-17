<template>
    <header>
        <h3>{{ title }}</h3>
    </header>
</template>

<script>

export default {
    name: 'Header',
    props: {
        title: String,
    }
}

</script>

<style scoped>
    header {
        margin-bottom: 15px;
    }

    h3 {
        font-size: 28px;
    }
</style>
