<template>
  <div class="newAlbum">
    <h1>新专速递</h1>

    <div class="playlist-row">
      <div class="playlists">
        <div class="item" v-for="album in albums" :key="album.id">
          <Cover
            :id="album.id"
            :type="'album'"
            :url="album.picUrl | resizeImage"
            :hoverEffect="true"
            :showBlackShadow="true"
          />

          <div class="text">
            <div class="name">{{ album.name }}</div>
            <div class="info">{{ album.artist.name }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { newAlbums } from "@/api/album";
import NProgress from "nprogress";

import Cover from "@/components/Cover.vue";

export default {
  data() {
    return {
      albums: [],
    };
  },
  components: {
    Cover,
  },
  created() {
    newAlbums({
      area: "EA",
      limit: 100,
    }).then((data) => {
      this.albums = data.albums;
      NProgress.done();
    });
  },
};
</script>

<style lang="scss" scoped>
h1 {
  span {
    color: rgba(0, 0, 0, 0.58);
  }
}

.playlist-row {
  margin-top: 36px;
  &:first-child {
    margin-top: 0;
  }
}
.playlists {
  display: flex;
  flex-wrap: wrap;
  margin: {
    right: -12px;
    left: -12px;
  }
  .index-playlist {
    margin: 12px 12px 24px 12px;
  }
}

.item {
  margin: 12px 12px 24px 12px;
  .text {
    width: 208px;
    margin-top: 8px;
    .name {
      font-size: 16px;
      font-weight: 600;
      color: rgba(0, 0, 0, 0.88);
      line-height: 20px;

      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
    .info {
      font-size: 12px;
      color: rgba(0, 0, 0, 0.68);
      line-height: 18px;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
      // margin-top: 4px;
    }
  }
}
</style>
