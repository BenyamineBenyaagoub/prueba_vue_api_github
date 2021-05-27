<template>
  <div>
    <b-modal v-model="modal">
      <div>
        <b-card no-body class="overflow-hidden w-100" style="max-width: 760px">
          <b-row no-gutters>
            <b-col md="6">
              <b-card-img
                :src="perfil.avatar_url"
                alt="Image"
                class="rounded-0"
              ></b-card-img>
            </b-col>
            <b-col md="6">
              <b-card-body :title="perfil.login">
                <b-card-text>
                  {{ perfil.bio }}
                </b-card-text>

                <a :href="perfil.html_url" class="btn btn-primary">
                  <fa icon="user" />
                  ver perfil
                </a>
              </b-card-body>
              
              <apexchart
                id="chart_bar"
                width="200"
                type="bar"
                :options="options"
                :series="[
                  {
                    name: ['Seguidores'],

                    data: [perfil.followers, perfil.following],
                  },
                ]"
              ></apexchart>
            </b-col>
          </b-row>
        </b-card>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: ["perfil", "modal"],
  data: () => ({
    options: {
      xaxis: {
        categories: ["Seguidores", "Seguidos"],
      },
    },
  }),
};
</script>