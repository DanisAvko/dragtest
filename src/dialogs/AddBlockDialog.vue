<template>
    <v-dialog v-model="show" persistent width="400">
        <v-card>
            <v-card-title>
                Карточка блока
            </v-card-title>
            <v-card-text>
                <v-text-field
                        label="Название"
                        v-model="title"
                        counter
                        maxlength="30"
                />
            </v-card-text>
            <v-card-actions>
                <v-spacer/>
                <v-btn
                        @click="addBlock()"
                        class="success"
                        :disabled="!title"
                >
                    Добавить
                </v-btn>
                <v-btn
                        class="error"
                        @click="closeDialog()"
                >
                    Отмена
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        name: "AddBlockDialog",
        props: {
            value: {
                type: Boolean,
            }
        },
        data: () => ({
            title: ''
        }),
        computed: {
            show: {
                get() {
                    return this.value
                },
                set(value) {
                    this.$emit('close', value)
                },
            },
        },
        methods: {
            addBlock() {
                this.$emit('addBlock', {
                    id: Date.now(),
                    title: this.title
                })
                this.closeDialog()
            },
            closeDialog() {
                this.show = false
                this.title = ''
            }
        }
    }
</script>