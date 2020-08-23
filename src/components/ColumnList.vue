<template>
    <v-container fluid>
        <v-btn class="ml-9 mt-3 mb-3"
               @click="openAddColumnDialog"
               title="Добавить столбец"
        >
            <v-icon>
                mdi-plus
            </v-icon>
        </v-btn>
        <draggable
                v-bind="dragOptions"
                v-model="columns"
                class="list-group column-container"
        >
            <div
                    v-for="column in columns"
                    :key="column.id"
                    class="column list-group-item"
            >
                <column
                        :column-data="column"
                        @deleteColumn="deleteColumn(column)"
                />
            </div>
        </draggable>
        <add-column-dialog
                :value="showAddColumnDialog"
                @close="value => showAddColumnDialog = value"
                @addColumn="addColumn"
        />
    </v-container>
</template>

<script>
    export default {
        name: "ColumnList",
        props: {
            items: {
                type: Array,
                required: true
            }
        },
        components: {
            Column: () => import('./Column'),
            AddColumnDialog: () => import('../dialogs/AddColumnDialog'),
            Draggable: () => import('vuedraggable')
        },
        data: () => ({
            showAddColumnDialog: false
        }),
        computed: {
            columns: {
                get() {
                    return this.items
                },
                set(value) {
                    this.$emit('setColumns', value)
                },
            },
            dragOptions() {
                return {
                    animation: 200,
                    group: "columns",
                };
            }
        },
        methods: {
            openAddColumnDialog() {
                this.showAddColumnDialog = true
            },
            setBlocks(column, payload) {
                column.blocks = payload
            },
            addColumn(payload) {
                this.$emit('addColumn', payload)
            },
            deleteColumn(column) {
                this.$emit('deleteColumn', column)
            }
        },
    }
</script>

<style scoped>
    .column-container {
        display: flex;
    }

    .column {
        flex-flow: row nowrap;
        min-width: 350px;
        max-width: 350px;
        margin: 10px;
        cursor: pointer;
    }
</style>