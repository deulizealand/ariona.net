<template>
  <div class="project" data-scroll>
    <div class="project-detail">
      <div class="project-year">{{resolvedDate}}</div>
      <h2 class="project-title">{{data.frontmatter.title}}</h2>
      <div class="project-desc">
        <p>{{data.frontmatter.summary}}</p>
      </div>
      <a class="project-link" :href="data.path">Learn More <span class="screen-reader-text">About {{data.frontmatter.title}}</span><i class="icon-arrow-right"></i></a>
    </div>
    <figure class="project-image" v-if="!data.frontmatter.scroller">

      <img-lazy :src="data.frontmatter.cover" alt="" :style="data.frontmatter.style" />
    </figure>
    <div class="project-image" v-else>
      <div class="image-scroller themezy" :style="{backgroundImage:`url(${data.frontmatter.cover})`}"></div>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
export default {
  props: {
    data: Object,
    imgStyle: Object,
  },
  computed: {
    resolvedDate() {
      return dayjs(this.data.frontmatter.date).format( 'YYYY' )
    },
  }
}
</script>

<style lang="scss">
.project {
  margin: 60px 0 100px;
  border-radius: 10px;
  display: flex;
  background: white;
  box-shadow: 0 1px 2px rgba(0,0,0,.1), 0 5px 20px rgba(0,0,0,.05);
  overflow: hidden;

  @media screen and (max-width: 768px) {
    flex-direction: column-reverse;
    margin-bottom: 30px;
  }
  /*
  transform: translate3d(0,30px,0);
  opacity: 0;
  transition: opacity .3s ease, transform .3s ease-out;
  transition-delay: .5s;

  &.is-inview {
    transform: translate3d(0,0,0);
    opacity: 1
  }
  */

  &.\--text-white{
    color: white;
  }

  &-detail {
    padding: 40px;
    display: flex;
    flex-direction: column;
    flex: 1;

    @media screen and (max-width: 768px) {
      padding: 30px;
    }
  }

  &-title{
    font-weight: 900;
    font-size: 3em;
    margin: 0 0 20px;
    // color: inherit;

    @media screen and (max-width: 768px) {
      font-size: 2em
    }
  }

  &-desc {
    flex: 1;
    padding-bottom: 30px;

    p:first-child{ margin-top: 0; }
    p:last-child{ margin-bottom: 0; }
  }

  &-link {
    display: flex;
    align-items: center;
    text-decoration: none;

    i {
      margin-left: 15px;
      font-size: 24px;
    }
  }

  &-image{
    align-self: flex-end;
    margin: 0;
    width: 50%;

    img{
      display: block;
    }

    @media screen and (max-width: 768px) {
      width: 100%;
      img {
        max-width: 100%;
        margin-left: 0!important;
      }
    }

    .image-scroller {
      padding-bottom: 80%;

      &.themezy{
        background-image: url("/assets/img/projects/themezy.jpg");
        animation: scroller 100s linear infinite alternate;
        background-size: cover;

        @media screen and (max-width: 768px) {
          animation: none;
        }
      }
    }
  }
}
@keyframes scroller {
  0% {
    background-position: top center;
  }
  50% {
    background-position: bottom center;
  }
  100% {
    background-position: top center;
  }
}
</style>