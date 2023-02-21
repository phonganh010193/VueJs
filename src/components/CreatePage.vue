<template>
    <div class="container mb-3">
        <form action="" class="d-flex justify-content-between">
            <div class="col-6">
                <div class="mb-3">
                    <lable for="" class="form-lable">Page Title</lable>
                    <input 
                        type="text"
                        class="form-control"
                        :value="pageTitle"
                        @input="(e) => pageTitle = e.target.value"
                    />
                </div>
                <div class="mb-3">
                    <lable for="" class="form-lable">Content</lable>
                    <textarea 
                        type="text"
                        class="form-control"
                        v-model="content"
                    ></textarea>
                </div>
                <div class="mb-3">
                    <button
                        class="btn btn-primary"
                        :disabled="isFormInvalid"
                        @click="submitForm"
                    >Create Page</button>
                </div>
            </div>
            <div class="col-5">
                <div class="mb-3">
                    <lable for="" class="form-lable">Link Title</lable>
                    <input 
                        type="text"
                        class="form-control"
                        v-model="linkTitle"
                    />
                </div>
                <div class="mb-3">
                    <lable for="" class="form-lable">Link Url</lable>
                    <input 
                        type="text"
                        class="form-control"
                        v-model="linkUrl"
                    />
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" v-model="published">
                        <lable class="form-check-lable" for="gridCheck1">Published</lable>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>
<script>
    export default {
        props:['pageCreated'],
        computed: {
            isFormInvalid() {
                return !this.pageTitle || !this.content || !this.linkTitle || !this.linkUrl
            }
        },
        data() {
            return {
                pageTitle: '',
                content:'',
                linkTitle: '',
                linkUrl: '',
                published: true
            }
        },
        methods: {
            submitForm() {
                if(!this.pageTitle || !this.content || !this.linkTitle || !this.linkUrl) {
                    alert('Please fill the form');
                    retrun ;
                }
                this.$emit('pageCreated', {
                    pageTitle: this.pageTitle,
                    content: this.content,
                    link: {
                        title: this.linkTitle,
                        url: this.linkUrl
                    },
                    published: this.published
                })
                this.pageTitle = '';
                this.content ='';
                this.linkTitle = '';
                this.linkUrl ='';
                published = true;
            },
            
        },
        watch: {
            pageTitle(newTitle, oldTitle) {
                if(this.linkTitle === oldTitle) {
                    this.linkTitle = newTitle;
                }
            }
        }
    }
</script>