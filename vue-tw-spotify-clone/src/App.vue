<template>

 <div class="bg-dark h-screen">
   <div class="flex" style="height:88vh;">
      <!-- side nav -->
      <div class="w-56 bg-black h-full flex-none">
          <div class="p-6">
            <img src="./assets/spotifyLogo.png" class="h-10" alt="logo" style="filter: brightness(0) invert(1);">
          </div>
          <div class="mx-2">
            <button v-for="page in pages" @click="setID = page.id" :key="page.id" :class="`w-full text-s font-semibold rounded px-3 py-2 flex items-center justify-start focus:outline-none ${setID === page.id ? 'bg-gray-800 text-white' : 'text-gray-100'}`">
              <i class="material-icons mr-3"> {{page.icon}} </i>
              <p> {{page.name}} </p>
            </button>
          </div>
          <div class="mx-5">
            <h1 class="mb-3 text-xs text-lightest tracking-widest uppercase">Playlists</h1>
            <button class="focus:outline-none flex items-center justify-start opacity-75 hover:opacity-100">
              <i class="material-icons h-8 w-8 mr-3 text-white pt-1">add_box</i>
              <p class="text-sm text-white font-semibold">Create Playlist</p>
            </button>
            <button class="focus:outline-none flex items-center justify-start opacity-75 hover:opacity-100">
              <i class="material-icons h-8 w-8 mr-3 text-white pt-1">favorite_border</i>
              <p class="text-sm text-white font-semibold">Liked Songs</p>
            </button>
            <div class="h-px w-full bg-gray-100 my-3"></div>
          </div>
          <div class="mx-5">
            <div class="w-full h-16 overflow-y-scroll">
              <p v-for="album in albums" :key="album" class="text-gray-500 hover:text-white text-hs py-1">{{ album.name }}</p>
            </div>
            <button class="flex items-center justify-start text-gray-500 hover:text-white py-2">
              <i class="material-icons mr-3 rounded-full border text-sm border-lightest">arrow_downward</i>
              <p class="text-sm font-semibold">Install App</p>
            </button>
          </div>
          <div class="relative pt-4">
            <div class="w-full h-full flex justify-end items-start opacity-0 hover:opacity-100 p-2 absolute">
              <div class="bg-black rounded-full h-6 w-6">
                <i class="material-icons text-white">keyboard_arrow_down</i>
              </div>
            </div>
            <img src="./assets/playing.jpg">
          </div>
      </div>
      <!-- main content -->
      <div class="w-full h-full relative bg-gray-900 overflow-y-scroll">
            <!-- header -->
        <div class="w-full sticky top-0 py-4 px-6 flex items-center justify-between bg-black z-10">
          <div class="flex items-center">
            <button class="focus:outline-none rounded-full bg-black w-8 h-8 text-white text-center mr-3">
              <i class="material-icons text-3xl pr-1">keyboard_arrow_left</i>
            </button>
            <button class="focus:outline-none rounded-full bg-black w-8 h-8 text-white text-center">
              <i class="material-icons text-3xl">keyboard_arrow_right</i>
            </button>
          </div>
          <div class="relative">
            <button @click="showDropdown = true" class="focus:outline-none bg-light rounded-full py-1 px-2 flex items-center">
              <img src="https://s.yimg.com/ny/api/res/1.2/7mV2p5kz.VA_i8Rr0oP4Dw--/YXBwaWQ9aGlnaGxhbmRlcjt3PTk2MDtoPTY0MA--/https://s.yimg.com/uu/api/res/1.2/H9bL0b5PzRUDELR4TWe6Rw--~B/aD04MDA7dz0xMjAwO2FwcGlkPXl0YWNoeW9u/https://media.zenfs.com/it/notizie_it_154/8058d59a96b893a39059500110d6b43b" class="rounded-full h-6 w-6 mr-2">
              <p class="text-white font-semibold text-xs mr-3">Rocco Siffredi</p>
              <i v-if="showDropdown === false" class="material-icons text-white">arrow_drop_down</i>
              <i v-if="showDropdown === true" class="material-icons text-white">arrow_drop_up</i>
            </button>
            <div v-if="showDropdown === true" class="absolute bg-gray-700 w-full rounded mt-1">
              <button @click="showDropdown = false" class="focus:outline-none w-full py-2 text-sm text-gray-500 hover:text-white border-white border-b-2 opacity-75 hover:opacity-100">Account</button>
              <button @click="showDropdown = false" class="focus:outline-none w-full py-2 text-sm text-gray-500 hover:text-white border-white">Log out</button>
            </div>
          </div>
        </div>
        <!-- Recently Played CARDS -->
        <div class="px-6 py-3">
          <div class="flex items-center justify-between pl-2">
            <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">Recently Played</h1>
            <h2 class="pr-8 text-xs text-gray-600 uppercase tracking-wider hover:underline">See All</h2>
          </div>

          <div class="w-full flex flex-wrap">
            <div v-for="recent in recents" :key="recent" class="p-2 w-48 relative">
              <div class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100">
                <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                  <i class="material-icons text-white text-2xl cursor-pointer">play_arrow</i>
                </div>
              </div>
              <div class="bg-gray-700 w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${ recent.src }`" class="h-auto w-full shadow mb-2">
                <h1 class="text-sm font-semibold text-white tracking-wide">{{ recent.title }}</h1>
                <h2 class="text-xs text-lightest tracking-wide pb-2">{{ recent.artist }}</h2>
              </div>
            </div>
          </div>
        </div>
        <!-- Made for you CARDS -->
        <div class="px-6 py-3">
          <div class="pl-2">
            <h1 class="text-2xl font-semibold text-white tracking-wider hover:underline">Made for you</h1>
            <h2 class="text-sm text-gray-600">Get better recommendations the more you listen</h2>
          </div>

          <div class="w-full flex flex-wrap">
            <div v-for="custom in customs" :key="custom" class="p-2 w-48 relative">
                <div class="absolute w-full h-full flex items-end justify-end p-8 opacity-0 hover:opacity-100">
                  <div class="bg-green rounded-full h-10 w-10 flex items-center justify-center">
                    <i class="material-icons text-white text-2xl">play_arrow</i>
                  </div>
                </div>
              <div class="bg-gray-700 w-full h-auto p-5 rounded-lg shadow-md">
                <img :src="`${ custom.src }`" class="h-auto w-full shadow mb-2">
                <h1 class="text-sm font-semibold text-white tracking-wide">{{ custom.title }}</h1>
                <h2 class="text-xs text-lightest tracking-wide pb-2">{{ custom.artist }}</h2>
              </div>
            </div>
          </div>
        </div>


      </div>
   </div>
   <!-- play bar -->
   <div class="w-full flex items-center justify-between px-3 bg-gray-800 border-t border-gray-900" style="height:12vh;">
     <div class="flex items-center">
       <div class="">
         <h1 class="text-sm text-white tracking-wide">Summer in the City - Remastered</h1>
         <h2 class="text-xs text-white tracking-wide">The Lovin' Spoonfull</h2>
       </div>
       <i class="material-icons text-base text-green mx-4">favorite</i>
       <i class="material-icons text-base text-white">picture_in_picture_alt</i>
     </div>
     <div class="flex flex-col justify-center w-2/5 items-center">
       <div class="flex items-center">
         <button class="text-gray-400 hover:text-white mx-5 focus:outline-none"><i class="material-icons text-lg ">shuffle</i></button>
         <button class="text-gray-400 hover:text-white focus:outline-none"><i class="material-icons text-lg">skip_previous</i></button>
         <button @click.prevent="playSong('.assets/song.mp3'), pause = true" class="rounded-full h-8 w-8 border-white border flex items-center justify-center mx-5 text-gray-400 hover:text-white focus:outline-none"><i v-if="pause === false" class="material-icons text-2xl">play_arrow</i><i v-if="pause === true" class="material-icons text-2xl">pause</i></button>
         <button class="text-gray-400 hover:text-white focus:outline-none"><i class="material-icons text-lg">skip_next</i></button>
         <button class="text-gray-400 hover:text-white mx-5 focus:outline-none"><i class="material-icons text-lg">repeat</i></button>
       </div>
       <div class="w-3/4 flex items-center justify-center mt-3">
         <p class="text-xs text-white mr-3">0:28</p>
         <div class="w-full h-1 bg-gray-400 rounded-full flex items-center">
            <div class="h-1 rounded-full bg-green" style="width: 18%;">

            </div>
            <div class="h-3 w-3 bg-white rounded-full -ml-1 shadow"></div>
          </div>
          <p class="text-xs text-white ml-3">2:40</p>

       </div>
     </div>
     <div class="flex items-center">
        <i class="material-icons text-base text-white mx-3">playlist_play</i>
        <i class="material-icons text-base text-white mx-3">important_devices</i>
        <i class="material-icons text-base text-white mx-3">volume_up</i>
        <div class="w-20 ml-3 bg-white rounded-full h-1"></div>
     </div>
   </div>
 </div>




</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      pages: [
        {id: 'home', name: 'Home', icon: 'home'},
        {id: 'search', name: 'Search', icon: 'search'},
        {id: 'library', name: 'Your Library', icon: 'bar_chart'}
      ],
      setID: 'home',
      albums: [
        {name: 'drive'},
        {name: 'zhu'},
        {name: 'All New Indie'},
        {name: 'Mellows'},
        {name: 'Classic Road Trip Songs'},
        {name: 'Lana Del Rey Radio'},
      ],
      showDropdown: false,
      recents: [
        {src:'https://i1.sndcdn.com/artworks-000170652608-dlyjaz-t500x500.jpg', title: 'Escape', artist: 'Sappheiros'},
        {src:'https://i.pinimg.com/736x/69/bc/cd/69bccd99bf05cd808790697f565486f7.jpg', title: 'Dark Forest', artist: 'Sappheiros'},
        {src:'https://i1.sndcdn.com/artworks-000326644047-1kflye-t500x500.jpg', title: 'Perception', artist: 'NF'},
        {src:'https://upload.wikimedia.org/wikipedia/en/thumb/b/b4/Encore_%28Eminem_album%29_coverart.jpg/220px-Encore_%28Eminem_album%29_coverart.jpg', title: 'Encore', artist: 'Eminem'},
        {src:'https://upload.wikimedia.org/wikipedia/en/f/f4/Ridetl.png', title: 'Ride the Lightning', artist: 'Metallica'},
        {src:'https://images-na.ssl-images-amazon.com/images/I/61BH%2BYWGniL._SL1088_.jpg', title: 'Clinic for Dolls', artist: 'Unsun'},
        {src:'https://upload.wikimedia.org/wikipedia/en/b/bb/Skrillex_-_Bangarang_%28EP%29.png', title: 'Bangarang', artist: 'Skrillex'},
        {src:'https://upload.wikimedia.org/wikipedia/en/6/66/Stronger_Cover.jpg', title: 'Stronger', artist: 'Dead by April'}
      ],
      customs: [
        {src:'https://upload.wikimedia.org/wikipedia/en/0/0c/Linkin_Park_Meteora_Album_Cover.jpg', title: 'Meteora', artist: 'Linkin Park'},
        {src:'https://upload.wikimedia.org/wikipedia/en/9/9b/Celebrity_Deathmatch_OST.jpg', title: 'Astonishing Pano..', artist: 'Marilyn Manson'},
        {src:'https://upload.wikimedia.org/wikipedia/en/4/48/Papa_Roach_Infest.jpg', title: 'Infest', artist: 'Papa Roach'},
        {src:'https://upload.wikimedia.org/wikipedia/en/thumb/7/7f/Santana_-_Supernatural_-_CD_album_cover.jpg/220px-Santana_-_Supernatural_-_CD_album_cover.jpg', title: 'Supernatural', artist: 'Santana'},
        {src:'https://upload.wikimedia.org/wikipedia/en/8/8c/Round_One.jpg', title: 'Round One', artist: 'Roy Jones Jr.'},
        {src:'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQp6Xmu__QQ50s0ViOiroleM6Nyrx3Xu4LJsA&usqp=CAU', title: 'Thug Revolution', artist: '2Pac'},
        {src:'https://upload.wikimedia.org/wikipedia/en/thumb/6/6c/TheOffspringPrettyFlyforaWhiteGuy.jpg/220px-TheOffspringPrettyFlyforaWhiteGuy.jpg', title: 'Pretty Fly for a w..', artist: 'The Offspring'},
        {src:'https://img.discogs.com/pDCyJjjS7XvZYQNCGcYjw4h1sak=/fit-in/300x300/filters:strip_icc():format(jpeg):mode_rgb():quality(40)/discogs-images/R-1995336-1497513530-9278.jpeg.jpg', title: 'Outta Control', artist: '50 Cent'}
      ],
      pause: false
    };
  },
  methods: {
    playSong(song) {
      if(song) {
        let audio = new Audio(song);
        audio.play();
      }
    }
  }
}
</script>

<style src="./assets/tailwind.css"/>
