<template>
  <div>
    <div>
      <router-link to="/"></router-link>
    </div>

    <div>
      <img :src="item.url" alt="">
    </div>
  </div>


</template>

<script>
  // @ is an alias to /src
  import $ from 'jquery';

  export default {
    name: "Item",
    props: {
      id: {
        type: String,
        required: true,
      }
    },
    data: function() {
      return {
        item: {}
      }
    },
    created: function () {
      const itemUrl = 'https://api.thecatapi.com/v1/images/' + this.id;

      console.log(this.id);
      $.ajax(itemUrl, {
        method: 'GET',
        headers: {
          'x-api-key' :  '6dd98ac3-a5c0-44ce-bb23-1f816ddbb071'
        },
      })
              .done((response) => {
                this.item = response;
              })
    }
  };
</script>

<style lang="scss" scoped>
  div {
    max-width: 800px;
    margin: 0 auto;
    height: 100%;
  }
  img {
    width: 100%;
  }
  a {
    border-radius: 50%;
    background: #f7f7f7;
    width: 50px;
    height: 50px;
    margin: 1.5rem 0;
    display: block;
    position: relative;
    text-align: center;
    &:before {
      border-top: 3px solid black;
      border-left: 3px solid black;
      content: '';
      width: 15px;
      height: 15px;
      display: block;
      position: absolute;
      top: 50%; left: 55%;
      transform: translate(-50%, -50%) rotate(-45deg);
    }
  }
</style>