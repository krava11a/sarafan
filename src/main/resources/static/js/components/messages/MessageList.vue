<template>
    <div style="position: relative; width: 300px;">
                <message-form :messages="messages" :messageAttr="message"></message-form>
        <message-row v-for="message in messages"
                     :key="message.id"
                     :message="message"
                     :editMessage="editMessage"
                     :deleteMessage="deleteMessage"
                     :messages="messages">
            {{message.text}}
        </message-row>
    </div>
</template>

<script>
    import MessageRow from "./MessageRow.vue";
    import MessageForm from "./MessageForm.vue";


    export default {
        components: {
            MessageRow, MessageForm
        },
        props: ['messages'],
        data() {
            return {
                message: null
            }
        },
        methods: {
            editMessage(message) {
                this.message = message;
            },
            deleteMessage(message) {
                this.$resource('/message{/id}').remove({id: message.id}).then(result => {
                    if (result.ok) {
                        this.messages.splice(this.messages.indexOf(message), 1);
                    }
                })
            }
        }
    }
</script>

<style>

</style>