<template >
  <div class="col-3">
    <b-card
      :title="perfil.id"
      :img-src="perfil.avatar_url"
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem"
      class="p-2 m-2"
    >
      <b-card-text>
         <fa icon="user" /> {{ perfil.login }}
      </b-card-text>

      <b-button @click="showMore(perfil.login)"  variant="primary"
        >Leer Más <fa icon="angle-double-right" /></b-button
      >
    </b-card>

    
  </div>
</template>

<script>
export default {
  props: ["perfil"],
  methods: {
    
    showMore(user){
      this.$emit('showProfile', user)

    }
  
  },

};
</script>