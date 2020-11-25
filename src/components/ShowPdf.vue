<template>
    <div class="showPdf">
        <div>
            <pdf
                    v-if="pdfSrc"
                    :src="pdfSrc"
                    :page="currentPage"
                    @num-pages="pageCount=$event"
                    @page-loaded="currentPage=$event"
                    @loaded="loadPdfHandler"
            ></pdf>
        </div>

        <p class="b_btn"  v-if="pdfSrc">
            <button @click="changePdfPage(0)" class="s_btn">上一页</button>
            {{currentPage}} / {{pageCount}}
            <button
                    @click="changePdfPage(1)"
                    class="s_btn"
            >下一页</button>
        </p>
    </div>
</template>

<script>
    import pdf from "vue-pdf";
    export default {
        name: "ShowPdf",
        components: {
            pdf
        },
        props: ["dochref", "doctype"],
        watch: {
            dochref(val) {
                console.log("pdfSrc");
                console.log(val);
                this.pdfSrc = val;
            },
            pdfSrc(val) {
                console.log(val+"watch")
            },
            doctype(typeval) {
                this.typeValue = typeval;
            },
            currentPage(val){
                console.log(val+"watch currentPage")
                this.currentPage = val;
            }
        },

        data() {
            return {
                typeValue: "",
                pdfSrc: "",
                currentPage: 1, // pdf文件页码
                pageCount: 0, // pdf文件总页数
                numPages: 0,
                activeIndex:0
            };
        },
        methods: {
            // 改变PDF页码,val传过来区分上一页下一页的值,0上一页,1下一页
            changePdfPage(val) {
                // 点击上一页 val=0;
                if (val === 0  && this.currentPage > 1) {
                    this.currentPage--;
                }
                if (val === 1 && this.currentPage < this.pageCount) {
                    this.currentPage++;
                }
            },
            // pdf加载时
            loadPdfHandler(e) {
                this.currentPage = 1; // 加载的时候先加载第一页
            }
        },
        mounted: function() {
            this.pdfSrc = "";
            this.pdfSrc = this.dochref;
        }
    };
</script>

<style scoped>
.b_btn{
    button{
        background-color: #42b983;
    }
    text-align: center;
    .s_btn{
        display: none;
        background-color: antiquewhite;
    }
}
</style>