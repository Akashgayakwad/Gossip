<template>
  <div class="feed" ref="feed">
    <ul v-if="contact">
      <li v-for="message in messages" :class="`message${message.to == contact.id ? ' sent' : ' recieved'}`" :key="message.id">
        <div class="text">
          {{message.text}}
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
  export default {
    props: {
      contact: {
        type: Object
      },
      messages: {
        type: Array,
        default: []
      }
    },
    methods: {
      scrollToBottom(){
        setTimeout(() => {
        this.$refs.feed.scrollTop = this.$refs.feed.scrollHeight - this.$refs.feed.clientHeight;
        },50);
      }
    },
    watch: {
      contact(contact) {
        this.scrollToBottom();
      },
      messages(messages){
        this.scrollToBottom();
      }
    }
  }
</script>
<style lang="scss" scoped>
.feed{
  background: aliceblue;
  min-height:370px;
  max-height:370px;
  overflow-y:scroll;
  ul{
    list-style-type: none;
    padding:10px;
    li{
      margin:10px 0;
      width:100%;
      &.sent{
        text-align:right;
        color:navy !important;
        .text{
          border-bottom-right-radius: 0px !important;
        }
      }
      &.recieved{
        text-align:left;
        color:brown !important;
        .text{
          border-bottom-left-radius: 0px !important;
        }
      }
      .text{
        max-width:250px;
        border-radius:25px;
        border: 1px solid black;
        padding:12px;
        display:inline-block !important;
      }
    }
  }
}
</style>
