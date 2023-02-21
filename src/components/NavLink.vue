<template>
    <a 
        class="nav-link" 
        :class="activeClasses"
        :href="page.link.url"
        :title="`This link goes to ${page.link.title}`"
    >{{page.link.title}}</a>
</template>
<script>
export default {
    props:['page', 'isActive'],
    computed: {
        activeClasses() {
            return {
                active: this.isActive,
                emphasize: this.isActive
            }
        }
    },
}
</script>
<style scoped>
    .emphasize{
        text-decoration: underline !important;
    }
</style>