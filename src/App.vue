<template>
  <div id="app">
    <p>hello</p>
    <ImgSlide :imageUrls="imageAction" :width="'300px'" :height="'300px'" />
  </div>

</template>
<script>

// import MySkill from './components/MySkill.vue'
import ImgSlide from './components/ImgSlide.vue'
export default {
  name: 'app',
  components: {
    ImgSlide
  },
  data () {
    return {
      imageUrls: [
        'https://i.natgeofe.com/k/ad9b542e-c4a0-4d0b-9147-da17121b4c98/MOmeow1_4x3.png',
        'https://images.unsplash.com/photo-1529778873920-4da4926a72c2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3V0ZSUyMGNhdHxlbnwwfHwwfHx8MA%3D%3D&w=1000&q=80',
        'https://hips.hearstapps.com/hmg-prod/images/beautiful-smooth-haired-red-cat-lies-on-the-sofa-royalty-free-image-1678488026.jpg?crop=0.88847xw:1xh;center,top&resize=1200:*'
      ],
      imageAction: [
        {
          url: 'https://i.natgeofe.com/k/ad9b542e-c4a0-4d0b-9147-da17121b4c98/MOmeow1_4x3.png',

          action: {
            type: 'link',
            url: 'https://hips.hearstapps.com/hmg-prod/images/beautiful-smooth-haired-red-cat-lies-on-the-sofa-royalty-free-image-1678488026.jpg?crop=0.88847xw:1xh;center,top&resize=1200:*'

          }
        },
        {
          url: 'https://images.unsplash.com/photo-1529778873920-4da4926a72c2?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3V0ZSUyMGNhdHxlbnwwfHwwfHx8MA%3D%3D&w=1000&q=80',
          action: {
            type: 'function',
            handler: () => {
              console.log('function ok!')
            }
          }
        },
        {
          url: 'https://hips.hearstapps.com/hmg-prod/images/beautiful-smooth-haired-red-cat-lies-on-the-sofa-royalty-free-image-1678488026.jpg?crop=0.88847xw:1xh;center,top&resize=1200:*',
          action: {
            type: 'function',
            handler: () => {
              console.log('function ok!')
            }
          }
        }

      ]
    }
  }
}

</script>
