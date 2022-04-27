<template>
    <div class="container">
        <SearchBar @termChange="termChange"/>
        <div class="row">
            <videoDetail :video="selectedVideo" />
            <video-list :videos="videos" @videoSelect="onVideoSelect"></video-list>
        </div>
    </div>
</template>

<script>
import SearchBar from './Components/SearchBar.vue';
import VideoList from './Components/VideoList.vue';
import axios from 'axios';
import VideoDetail from './Components/VideoDetail.vue';

const API_KEY = 'AIzaSyCgAQ908MDz2yK28BVpYUNFnC9n-4OC5JQ';

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data() {
        return {
            videos: [],
            selectedVideo: null,
        }
    },
    methods: {
        termChange(input) {
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: input
                }
            })
            .then((response) => {
                this.videos = response.data.items;
            })
        },
        onVideoSelect(video) {
            this.selectedVideo = video;
        }
    }
}
</script>
