<template>
  <Layout :sidebar="false">
    <div class="content">
      <h1>{{ $static.metadata.siteName }} - {{ this.description }}</h1>
      <nav>
        <!-- To use other icons here, you need to import them in the Shortcut component -->
        <Shortcut link="/about" text="About" icon="star-icon" />
        <Shortcut link="/getting-started" text="Getting Started" icon="play-icon" />
        <Shortcut link="/arduino-library" text="Arduino Library" icon="cpu-icon" />
      </nav>
      
    </div>

    <div id="stats_img">
        <img src="https://console.tabahi.tech/stats/1.png">
    </div>
  </Layout>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import Shortcut from '~/components/Shortcut.vue'

export default {
  components: {
    Shortcut
  },
  data() {
    return {
      description: 'The ultimate cloud to control your IoT devices'
    }
  },
  metaInfo() {
    return {
      title: this.description,
      meta: [
        { key: 'description', name: 'description', content: 'A cloud service to easily manage, control, communicate with your IoT devices using our arduino library.' }
      ]
    }
  }
}
</script>



<style lang="scss" scoped>
.content {
  display: flex;
  flex-direction: column;
}

h1 {
  text-align: center;
  max-width: 600px;
  margin: 1.5em auto 1.5em;

  @include respond-above(md) {
    max-width: 1000px;
  }
}

h2 {
  font-size: 1.4rem;
  margin: 0;
}

nav {
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  @include respond-above(sm) {
    flex-direction: row;
  }
}

.git {
  margin: 3em 0 0;
  align-self: center;

  @include respond-above(md) {
    margin: 5em 0 0;
  }
}
</style>
