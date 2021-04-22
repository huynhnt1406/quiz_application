<template>
    <b-navbar toggleable type="dark" variant="dark" class="mt-5">
        <b-navbar-brand href="#">Quiz Application</b-navbar-brand>
        <b-navbar-brand href="#">{{numCorrect}} / {{numTotal}}</b-navbar-brand>
    </b-navbar>
</template>
<script>
export default {
    name:"Header",
    props:['numCorrect','numTotal']

}
</script>
<style >
    
</style>