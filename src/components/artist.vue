<template lang="pug">

      li.artist
        h3: a(:href="artist.url" target="_blank") {{artist.name}}
        //- h2 {{artist.name}}
        //- a(:href="''" target="_blank") {{ artist.url }}
        img(:src="artist.image[2]['#text']")
        //img(src="./assets/logo.png")

      

</template>

<script>

export default {
    name: 'artist',
    props: ['artist']
  }

</script>
// <style lang="stylus" scoped>
//   li.artist
//     display block
//     margin 10px 0

// </style>


