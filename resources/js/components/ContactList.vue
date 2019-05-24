<template>
  <div class="contacts-list">
      <ul>
        <li v-for="(contact, index) in contacts" :key="contact.id" @click="selectedContact(index,contact)" :class="{'selected':index == selected }">
          <div class="avatar">
            <img :src="contact.profile_image" :alt="contact.name"/>
          </div>
          <div class="contact">
            <p class="name">{{contact.name}}</p>
            <p class="email">{{contact.email}}</p>
          </div>
        </li>
      </ul>
  </div>
</template>
<script>
  export default{
    props:{
      contacts:{
        type: Array,
        default: []
      }
    },
    data() {
      return {
        selected : 0,
      };
    },
    methods: {
      selectedContact(index, contact){
        this.selected = index;
        this.$emit('selected', contact);
      }
    }
  }
</script>

<style lang="scss" scoped>
.contacts-list{
  flex: 2;
  max-height: 480px;
  overflow-y:scroll;
  border-left: 1px solid gray;
}
ul{
  list-style-type:none;
  padding-left:0;
}
li{
  display:flex;
  padding: 2px;
  height:80px;
  position:relative;
  border-bottom: 1px solid grey;
  cursor: pointer;
  &.selected{
      background: darkseagreen;
      color:linen;
  }
}
.avatar{
  flex:1;
  display:flex;
  align-items:center;
}
.avatar img{
  width:50px;
  border-radius: 50%;
  margin: 0 auto;
}
.contact{
  flex:3;
  font-size:10px;
  overflow:hidden;
  display:flex;
  flex-direction: column;
  justify-content: center;
}
.contact p{
  margin: 0;
}
.contact .name{
  font-weight:bold;
}

</style>
