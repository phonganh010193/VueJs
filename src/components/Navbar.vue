<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg', 'd-flex', 'justify-content-between']"
    >
        <div class="d-flex">
            <div class="navbar-header">
                <a class="navbar-brand" href="#">My Vue</a>
            </div>
            <ul class="navbar-nav">
                <li class="nav-item" v-for="(page, index) in publishedPages" :key="index">
                    <nav-link
                        :isActive="activePage === index"
                        :page="page"
                        @click.prevent="navLinkClick(index)"
                    ></nav-link>
                    
                </li>
            </ul>
        </div>
        <div>
            <button 
                class="btn btn-primary"
                @click.prevent="changeTheme()"
            >Toggle NavBar</button>
        </div>
    </nav>
</template>
<script>
    import NavLink from '../components/NavLink.vue';
    export default {
        components:{
            NavLink
        },
        created() {
            this.getThemeSetting()
        },
        computed: {
            publishedPages() {
                return this.pages.filter(el => el.published)
            }
        },
        props:['pages', 'activePage', 'navLinkClick'],
        data() {
            return {
                theme: 'light',
            }
        },
        methods: {
            changeTheme() {
                let theme = 'light'
                if(this.theme == 'light') {
                    theme = 'dark'
                }
                this.theme = theme;
                this.storeThemeSetting()
            },
            storeThemeSetting() {
                localStorage.setItem('theme', this.theme)
            },
            getThemeSetting() {
                let theme = localStorage.getItem('theme');
                if(theme) {
                    this.theme = theme;
                }
            }
        },
    }
</script>