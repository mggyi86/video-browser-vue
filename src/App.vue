<template>
  <div class="container">
    <SearchBar @termChange="termChange"></SearchBar>
    <div class="row">
      <VideoDetail :video="selectedVideo"></VideoDetail>
      <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
    </div>
    <!-- <pre>
      {{$data}}
    </pre> -->
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from './components/SearchBar'
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'

const API_KEY = 'AIzaSyBEkFhZ7vi9VoMuhWioHbEQoMCiyiEv8P4'

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data: function () {
    return {
      videos: [],
      selectedVideo: {}
    }
  },
  methods: {
    termChange: function (searchTerm) {
      axios.get('https://www.googleapis.com/youtube/v3/search', {
        params: {
          key: API_KEY,
          type: 'video',
          part: 'snippet',
          q: searchTerm
        }
      }).then(response => {
        this.videos = response.data.items
      })
    },
    onVideoSelect: function (video) {
      this.selectedVideo = video
    }
  }
}
</script>
