<template lang="pug">
Carousel(:itemList="imageList" height="400px" width="400px" style="width: 900px")
  template(#item="{item}")
    div(style="height:100%; display:flex; align-items: center; backdrop-filter: blur(10px);" :style="{backgroundImage: `url(${item})`}")
      img(:src="item" style="width:100%;")
</template>

<script>
import Carousel from './components/Carousel.vue'

export default {
  name: 'App',
  components: {
    Carousel
  },
  setup () {
    return {
      imageList: [
        'https://images.unsplash.com/photo-1632529800649-faf2f6e7dff3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5Njk1Ng&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1632769092277-83b8c526a673?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4OA&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1633005619804-8b6124945cfb?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4Nw&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1632725514221-b1c217475d92?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4NQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1627562369448-bc40100a959b?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4NA&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1632715413694-0842be6fa2b0?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4Mw&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1634150872460-b97af031c991?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI4MQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1634151296702-962d96fe5a18?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTI3OQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1632504102499-7dc472b50653?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1Nw&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1633760538186-c239ab18f545?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1Ng&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1634571798961-bf45f97a78e8?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1NQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1633102575634-dc72edadd467?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1NA&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1633793545207-bd5a09c3e4a5?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1MQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1634938971687-1082b4cb018c?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM1MA&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1633176036492-706dd11c57b3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM0OQ&ixlib=rb-1.2.1&q=80&w=1080',
        'https://images.unsplash.com/photo-1632830025073-3da7ac07402b?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxfDB8MXxyYW5kb218MHx8fHx8fHx8MTYzNTE5OTM0Nw&ixlib=rb-1.2.1&q=80&w=1080',
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
}
</style>
