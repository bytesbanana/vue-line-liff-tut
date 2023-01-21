<template>
  <div className="layout">
    <img alt="Profile" v-bind:src="profilePic" width="100" height="100" />

    <h1>{{ displayName }}</h1>
    <p>{{ statusMessage }}</p>
  </div>
</template>

<script>
import liff from '@line/liff';

export default {
  name: 'App',
  components: {},
  async beforeCreate() {
    liff.ready.then(async () => {
      if (liff.isInClient()) {
        await this.getProfilePic();
      }
    });
    await liff.init({
      liffId: '1657838953-QPY6AODk',
    });
  },
  methods: {
    async getProfilePic() {
      const profile = await liff.getProfile();
      this.profilePic = profile.pictureUrl;
      this.displayName = profile.displayName;
      this.statusMessage = profile.statusMessage;
    },
  },
  data() {
    return {
      profilePic: 'https://cdn-icons-png.flaticon.com/512/21/21104.png',
      displayName: 'Loading...',
      statusMessage: '',
    };
  },
};
</script>

<style>
.layout {
  display: flex;
  border: 5px solid salmon;
  border-radius: 10px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}
img {
  border-radius: 50%;
}
p {
  color: #808080;
}
</style>
