<template>
    <v-app :dark="setTheme">
        <v-app-bar app clipped-left color="deep-purple darken-1" dark>
            <div class="d-flex align-center">
                <v-app-bar-nav-icon class="hidden-lg-and-up" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
                <router-link to="/">
                    <v-img :src="require('../src/assets/header-logo.svg')" alt="" class="shrink mr-2" contain transition="scale-transition" width="32" />
                </router-link>
                <router-link to="/">
                    <v-img
                        :src="require('../src/assets/header-logo--txt-wh.svg')"
                        alt=""
                        class="shrink mr-2 hidden-sm-and-down"
                        contain
                        min-width="80"
                        width="80"
                    />
                </router-link>
                <router-link to="/">
                    <v-img :src="require('../src/assets/header-logo--docs.svg')" alt="" class="shrink " contain min-width="48" width="48" />
                </router-link>
            </div>

            <v-spacer></v-spacer>

            <v-btn text href="https://www.payple.kr/" target="_blank" class="mx-2 d-none d-sm-flex">
                <v-icon class="mr-2">mdi-home-outline</v-icon> 페이플 홈페이지
            </v-btn>
            <v-btn text href="https://www.payple.kr/?ACT_=demo" target="_blank" class="mx-2 d-none d-sm-flex">
                <v-icon class="mr-2">mdi-book-play-outline</v-icon> 페이플 데모
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" app clipped>
            <v-list dense>
                <v-treeview :items="navi" openOnClick open-all>
                    <template slot="label" slot-scope="props">
                        <router-link :to="props.item.to" v-if="props.item.to">{{ props.item.name }}</router-link>
                        <span v-else>{{ props.item.name }}</span>
                    </template>
                </v-treeview>
            </v-list>

            <template v-slot:append>
                <div class="pa-2">
                    <v-switch :label="`어두운 테마`" v-model="goDark"></v-switch>
                </div>
            </template>
        </v-navigation-drawer>

        <v-main>
            <v-container style="max-width: 1000px;">
                <router-view></router-view>
                <v-divider class="mb-12"></v-divider>
                <v-row class="mb-12 pt-12">
                    <v-col col="12" sm="4">
                        <router-link class="no-style-link" to="/faq">
                            <v-card>
                                <v-list-item>
                                    <v-list-item-avatar color="pink darken-1">
                                        <v-icon color="white">
                                            mdi-frequently-asked-questions
                                        </v-icon>
                                    </v-list-item-avatar>

                                    <v-list-item-content>
                                        <v-list-item-title class=" mb-2">FAQ</v-list-item-title>
                                        <v-list-item-subtitle>높은 빈도의 문의를 모아봤어요</v-list-item-subtitle>
                                    </v-list-item-content>
                                    <!-- <v-list-item-action>
                                        <v-btn fab text color="blue accent-4">
                                            <v-icon>
                                                mdi-vector-link
                                            </v-icon>
                                        </v-btn>
                                    </v-list-item-action> -->
                                </v-list-item>
                            </v-card>
                        </router-link>
                    </v-col>
                    <v-col col="12" sm="4">
                        <a class="no-style-link" href="https://github.com/PAYPLECORP" target="_blank">
                            <v-card>
                                <v-list-item>
                                    <v-list-item-avatar color="indigo darken-4">
                                        <v-icon color="white">
                                            mdi-git
                                        </v-icon>
                                    </v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class=" mb-2">GITHUB</v-list-item-title>
                                        <v-list-item-subtitle>페이플 오픈 소스에 참여 하세요</v-list-item-subtitle>
                                    </v-list-item-content>
                                    <!-- <v-list-item-action>
                                        <v-btn fab text color="blue accent-4">
                                            <v-icon>
                                                mdi-vector-link
                                            </v-icon>
                                        </v-btn>
                                    </v-list-item-action> -->
                                </v-list-item>
                            </v-card>
                        </a>
                    </v-col>
                    <v-col col="12" sm="4">
                        <a class="no-style-link" href="mailto:dev@payple.kr">
                            <v-card>
                                <v-list-item>
                                    <v-list-item-avatar color="teal accent-4">
                                        <v-icon color="white">
                                            mdi-email-send-outline
                                        </v-icon>
                                    </v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class=" mb-2">MAIL</v-list-item-title>
                                        <v-list-item-subtitle>페이플 개발팀에 문의해보세요</v-list-item-subtitle>
                                    </v-list-item-content>
                                    <!-- <v-list-item-action>
                                        <v-btn fab text color="blue accent-4">
                                            <v-icon>
                                                mdi-pencil
                                            </v-icon>
                                        </v-btn>
                                    </v-list-item-action> -->
                                </v-list-item>
                            </v-card>
                        </a>
                    </v-col>
                </v-row>
            </v-container>
        </v-main>

        <v-footer app inset absolute align-center class=" pa-4"> &copy;{{ new Date().getFullYear() }} — <strong>PAYPLE</strong> </v-footer>
    </v-app>
</template>

<script>
export default {
    name: "App",
    opts: {
        theme: {
            dark: false,
        },
    },
    data: () => ({
        drawer: null,
        group: null,
        // drawer end
        goDark: false,
        // dark theme end
        hidden: false,
        // float button end
        navi: [
            {
                id: 1,
                name: "UI커스텀 결제",
                children: [
                    {
                        id: 1 - 0,
                        name: "개요",
                        to: "/ui/outline",
                    },
                    {
                        id: 1 - 1,
                        name: "환경설정",
                        children: [
                            { id: 1 - 1 - 1, name: "환경설정 개요", to: "/ui/install/outline" },
                            { id: 1 - 1 - 2, name: "상황별 인증 요청 방식", to: "/ui/install/auth" },
                        ],
                    },
                    {
                        id: 1 - 2,
                        name: "API",
                        children: [
                            { id: 1 - 2 - 0, name: "카드등록", to: "/ui/regist/card" },
                            { id: 1 - 2 - 1, name: "결제요청", to: "/ui/pay/request" },
                            { id: 1 - 2 - 2, name: "결제요청 (월 중복결제 방지)", to: "/ui/pay/regular-refuse" },
                            { id: 1 - 2 - 3, name: "승인취소", to: "/ui/pay/cancel" },
                            { id: 1 - 2 - 4, name: "등록카드 해지", to: "/ui/regist/cancel" },
                            { id: 1 - 2 - 5, name: "등록카드 조회", to: "/ui/regist/search" },
                            { id: 1 - 2 - 6, name: "결제결과 조회", to: "/ui/result/search" },
                            { id: 1 - 2 - 7, name: "응답코드", to: "/ui/code/response" },
                            { id: 1 - 2 - 8, name: "정책", to: "/ui/policy" },
                        ],
                    },
                ],
            },
            {
                id: 2,
                name: "웹훅 URL 설정",
                to: "/webhook",
            },
            {
                id: 3,
                name: "샘플코드",
                to: "/code/sample",
            },
            {
                id: 4,
                name: "문서 버전",
                to: "/docs-ver",
            },
            {
                id: 5,
                name: "FAQ",
                to: "/faq",
            },
        ],
    }),

    computed: {
        setTheme() {
            if (this.goDark == true) {
                return (this.$vuetify.theme.dark = true);
            } else {
                return (this.$vuetify.theme.dark = false);
            }
        },
    },

    watch: {
        group() {
            this.drawer = false;
        },
        top(val) {
            this.bottom = !val;
        },
        right(val) {
            this.left = !val;
        },
        bottom(val) {
            this.top = !val;
        },
        left(val) {
            this.right = !val;
        },
    },
};
</script>


<style scoped>
.v-treeview a {
    color: rgba(0, 0, 0, 0.87);
    text-decoration: none;
}
.v-treeview a.router-link-active {
    color: #1867c0;
}
.theme--dark .v-treeview a {
    color: #fff;
}
.theme--dark .v-treeview a.router-link-active {
    color: #1867c0;
}
</style>

<style>
* {
    font-family: "Noto Sans KR", sans-serif !important;
}
table {
    white-space: normal;
    text-align: center;
    word-break: keep-all;
    min-width:100%;
}
table td {
    border: 1px solid rgba(0, 0, 0, 0.06);
}
table th {
    border: 1px solid rgba(0, 0, 0, 0.06);
    border-collapse: collapse;
    font-weight: 700;
    font-size: 1rem !important;
    text-align: center !important;
}
@media screen and (min-width: 0px) and (max-width: 720px) {
    table {
        white-space: nowrap;
        text-align: center;
        word-break: keep-all;
    }
}
.limit table {
    white-space: normal;
    max-width: 100%;
}
.temp_table.no_th th{
    display:none !important;
}
.half-bg--payple {
    position: relative;
    display: inline;
}
.half-bg--payple:before {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 60%;
    background: rgba(120, 82, 232, 0.4);
    z-index: 0;
    border-radius: 4px;
}
.half-bg--tooltip {
    position: relative;
    display: inline;
}
.half-bg--tooltip:before {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 60%;
    background: rgba(41, 98, 255, 0.4);
    z-index: 0;
    border-radius: 4px;
}
.white-space-normal {
    white-space: normal !important;
}
.word-break-keep-all {
    word-break: keep-all;
}
.word-break-break-all {
    word-break: break-all;
}
pre {
    margin: 0 !important;
    padding: 0 !important;
}
code {
    width: 100%;
    margin: 0;
    padding: 0 1rem;
    font-weight: 400 !important;
}
.tree-gutter {
    display: inline-block;
    width: 20px;
}
.cursor-pointer {
    cursor: pointer;
}
.no-style-link {
    color: inherit !important;
    text-decoration: none !important;
}
</style>