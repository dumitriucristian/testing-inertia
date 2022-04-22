<template>
    Hello world {{name}} sdfsf
    <li v-for="framework in frameworks" > test {{framework}} ssss</li>
    <p>ss</p>
</template>
<script>
//props must be declared before use
export default {
    props: {
        name: String,
        frameworks: Array
    }
}
</script>
