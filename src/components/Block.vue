<template>
    <v-card>
        <v-card-title>
            <div class="column-title">
                {{blockData.title}}
            </div>
            <v-spacer/>
            <v-btn
                    icon
                    title="Удалить"
                    @click="deleteBlock"
            >
                <v-icon>
                    mdi-close
                </v-icon>
            </v-btn>
        </v-card-title>
        <v-card-text>
            Какой-то контент
        </v-card-text>
    </v-card>
</template>

<script>
    export default {
        name: "Block",
        props: {
            blockData: {
                type: Object,
                required: true
            },
        },
        methods: {
            deleteBlock() {
                this.$emit('deleteBlock')
            }
        }
    }
</script>

<style scoped>
    .column-title {
        word-break: break-all;
        max-width: 70%;
    }
</style>