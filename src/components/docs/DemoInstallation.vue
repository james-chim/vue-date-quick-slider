<template>
  <div>
    <h1 class="my-3">Installation</h1>
    <p>To install this library, run the following command.</p>
    <b-alert show variant="secondary">
      <code>
        $ npm install --save vue-date-quick-slider
      </code>
    </b-alert>
    <p>Add the following lines to your repository</p>
    <b-alert show variant="secondary">
      <code>
        import dateQuickSlider from 'vue-date-quick-slider';<br/><br/>
        export default {<br/>
        &emsp;&emsp;// ...<br/>
        &emsp;&emsp;components: {<br/>
        &emsp;&emsp;&emsp;&emsp;dateQuickSlider<br/>
        &emsp;&emsp;}<br/>
        &emsp;&emsp;// ...<br/>
        }
      </code>
    </b-alert>
  </div>
</template>

<script>
  export default {
    name: 'DemoInstallation',
    data () {
      return {
      }
    }
  }
</script>

<style>
</style>
