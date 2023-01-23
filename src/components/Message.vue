<template>
    <div id="message">
        <p>{{ msg }}</p>
    </div>
</template>
<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>
<style scoped>
#message {
    margin:auto;
    padding: 10px;
    background-color: rgb(88, 152, 226);
    color: #cde9ec;
    border-top: 2px solid rgb(77, 87, 230);
    width: 400px;
    margin-bottom: 30px;
    border-radius: 5px;
}
</style>
