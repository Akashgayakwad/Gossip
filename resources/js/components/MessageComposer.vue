<template>
  <div class="composer">
    <textarea v-model="message" @keydown.enter="send" placeholder="Type a Message..."></textarea>
  </div>
</template>
<script>
  export default {
    data(){
      return {
        message: ""
      };
    },
    methods:{
      send(e){
        e.preventDefault();
        if(this.message== ''){
          return ;
        }
        this.$emit('send',this.message);
        this.message = "";
      }
    }
  }
</script>
<style lang="scss" scoped>
.composer textarea{
  width:90%;
  margin:10px;
  resize:none;
  border-radius:3px;
  border: 3px solid lightgray;
  padding: px;
}
</style>
