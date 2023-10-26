<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-avatar>
          <v-img :src="imageProfile" />
        </v-avatar>
      </v-col>
      <v-col cols="12">
        <div>Display Name: {{ displayName }}</div>
        <div>UserID: {{ userId }}</div>
      </v-col>
    </v-row>
    <v-overlay :value="loading"></v-overlay>
  </v-container>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
      loading: false,
      imageProfile: '',
      displayName: '',
      userId: '',
    }
  },
  mounted() {
    this.initLiff()
  },
  methods: {
    async initLiff() {
      await this.$liff.init({
          liffId: '1654097973-D7rnQmw9',
          withLoginOnExternalBrowser: true,
      });
      console.log('initialized')
      await this.getProfile()
    },
    async getProfile() {
      try {
        this.loading = true
        const profile = await this.$liff.getProfile()
        this.userId = profile.userId
        this.displayName = profile.displayName
        this.imageProfile = profile.pictureUrl
      } catch (error) {
        console.error(error)
      } finally {
        this.loading = false
      }
    }
  }
}
</script>
