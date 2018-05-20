<template>
  <div>
    <b-navbar toggleable="md" type="dark" variant="info">
      <b-container>
        <b-navbar-brand href="#">Vue Date Quick Slider</b-navbar-brand>
      </b-container>
    </b-navbar>

    <b-container>
      <demo-introduction></demo-introduction>
      <demo-installation></demo-installation>
      <demo-date-quick-slider></demo-date-quick-slider>
      <footer-brand></footer-brand>
    </b-container>
  </div>
</template>

<script>
  import DemoIntroduction from '@/components/docs/DemoIntroduction'
  import DemoInstallation from '@/components/docs/DemoInstallation'
  import DemoDateQuickSlider from '@/components/docs/DemoDateQuickSlider'
  import FooterBrand from '@/components/docs/FooterBrand'

  export default {
    name: 'Demo',
    components: {
      DemoIntroduction,
      DemoInstallation,
      DemoDateQuickSlider,
      FooterBrand
    }
  }
</script>

<style>
</style>
