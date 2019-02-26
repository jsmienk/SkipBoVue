<template>
    <div id="header">
        <h1 class="title"><slot></slot></h1>
    </div>
</template>

<script>
export default {
    data() {
        return {}
    }
}
</script>

<style lang="scss">
#header {
    text-align: left;
    padding: 16px 32px;
    background-color: #1a1a1a;
}

.title {
    margin: 0;
    font-weight: bold;
    font-size: 2.5em;
}
</style>
