<template>
    <div class="v-table">
        <div class="v-table_header">
            <p @click="sortByName">Name
                <i class="material-icons">
                    swap_vert
                </i>
            </p>
            <p @click="sortByPoint">Points earned
                <i class="material-icons">
                    swap_vert
                </i>
            </p>
            <p @click="sortBySpent">Points spent
                <i class="material-icons">
                    swap_vert
                </i>
            </p>
            <p @click="sortByData">Registration date
                <i class="material-icons">
                    swap_vert
                </i>
            </p>
        </div>
        <div class="v-table_body">
            <v-table-row
                    v-for="row in paginatedUsers"
                    :key="row.id"
                    :row_data="row"
            />
        </div>
        <!--        pgination-->
        <div class="v-table_pagination">
            <div class="page" v-for="page in pages" :key="page"
                 @click="pageClick(page) "
                 :class="{'page_selected': page === pageNumber}">
                {{page}}
            </div>
        </div>
    </div>
</template>

<script>
    import VTableRow from "./v-table-row";

    export default {
        name: "v-table",
        components: {VTableRow},
        props: {
            users_data: {
                type: Array,
                default: () => {
                    return []
                }
            }
        },
        data() {
            return {
                usersPerPage: 15,
                pageNumber: 1,
            }
        },
        computed: {
            pages() {
                return Math.ceil(this.users_data.length / 20)
            },
            paginatedUsers() {
                let from = (this.pageNumber - 1) * this.usersPerPage;
                let to = from + this.usersPerPage;
                return this.users_data.slice(from, to)

            }
        },
        methods: {
            pageClick(page) {
                this.pageNumber = page;
            },
            // sort
            sortByName() {
                this.users_data.sort((a, b) => a.name.localeCompare(b.name))
            },
            sortByPoint() {
                this.users_data.sort((a, b) => a.points_earned - b.points_earned)
            },
            sortBySpent() {
                this.users_data.sort((a, b) => a.points_spent - b.points_spent)
            },
            sortByData() {
                this.users_data.sort((a, b) => a.registration_date.localeCompare(b.registration_date))
            }
        }

    }
</script>

<style scoped>
    .v-table {
        max-width: 900px;
        margin: 0 auto;
    }

    .v-table_header {
        display: flex;
        justify-content: space-around;
        border-bottom: solid 1px #e7e7e7;
    }

    .v-table_header p {
        display: flex;
        align-items: center;
        flex-basis: 25%;
        text-align: left;
        cursor: pointer;
    }

    .v-table_pagination {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 25px;
    }

    .page {
        padding: 8px;
        border: solid 1px #e7e7e7;

        margin-right: 10px;
    }

    .page:hover {
        background: cadetblue;
        cursor: auto;
    }

    .page_selected {
        background: cadetblue;
        cursor: auto;
        color: #e7e7e7;
    }
</style>