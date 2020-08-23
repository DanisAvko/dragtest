<template>
    <v-app>
        <v-container class="app-container" fluid>
            <column-list
                    :items="columns"
                    @addColumn="addColumn"
                    @deleteColumn="deleteColumn"
                    @setColumns="setColumns"
            />
        </v-container>
    </v-app>
</template>

<script>
    export default {
        name: 'App',
        components: {
            ColumnList: () => import('./components/ColumnList')
        },
        data: () => ({
            columns: [],
        }),
        methods: {
            setColumns(payload) {
                this.columns = payload
            },
            addColumn(payload) {
                this.columns.unshift(payload)
            },
            deleteColumn(column) {
                let delIndex = this.columns.findIndex(item => item.id === column.id)
                this.columns.splice(delIndex, 1)
            },
        },
        mounted() {
            import('./mocks/columns.json')
                .then(response => {
                    this.columns = response.columns
                })
        }
    };
</script>

<style scoped>
    .app-container {
        overflow: auto;
        height: 100vh
    }
</style>
