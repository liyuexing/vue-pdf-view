<template>
    <div class="hello">
<!--        {{msg}}-->
        <showPdf
                v-if="docInfo.type == 'pdf'"
                :doctype="docInfo.type"
                :dochref="docInfo.href"
        ></showPdf>
    </div>
</template>

<script>
    // @ is an alias to /src
    import ShowPdf from '@/components/ShowPdf.vue'
    export default {
        name: "PdfView",
        components:{
            ShowPdf
        },
        data () {
            return {
                msg: 'Welcome to Your Vue.js App',
                docInfo: {
                    type: "pdf",
                    href: "http://image.cache.timepack.cn/nodejs.pdf"
                },
            }
        },
        mounted(){
        }
    }
</script>

<style scoped>

</style>