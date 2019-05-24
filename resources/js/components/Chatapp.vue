<template>
  <div class="chat-app">
     <Conversation :contact='selectedContact' :messages="messages" @new="saveNewMessage"/>
     <ContactsList :contacts="contacts" @selected="startConversationWith"/>
  </div>
</template>

<script>
  import Conversation from './Conversation';
  import ContactsList from './ContactList';
    export default {
      props:{
          user:{
            type: Object,
            required: true
          }
      },
      data(){
        return {
            selectedContact: null,
            messages: [],
            contacts: []
        };
      },
        mounted() {
            Echo.private(`messages.${this.user.id}`)
              .listen('NewMessage', (e) => {
                  console.log('listened');
                  this.handleIncoming(e.message);
              })
            axios.get('/contacts')
            .then((response) => {
              this.contacts = response.data;
            });
        },
        methods:{
          startConversationWith(contact){
            axios.get(`/conversation/${contact.id}`)
            .then((response)=> {
              console.log(response);
              this.messages = response.data;
              this.selectedContact = contact;
            });
          },
          saveNewMessage(text){
            console.log(this.messages);
            this.messages.push(text);
            console.log(this.messages);
          },
          handleIncoming(message){
            if(this.selectedContact && message.from == this.selectedContact.id){
              this.saveNewMessage(message);
            }

            alert(message.text);
          }
        },
        components: {Conversation, ContactsList}
    }
</script>

<style lang="scss" scoped>
  .chat-app{
    display:flex;
  }
</style>
