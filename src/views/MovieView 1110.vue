<template>
  <div>
    <HeaderCont />
    <TitleCont name1="movie" name2="reference api" />
    <section class="cont__refer">
      <div class="container">
        <div class="movie__inner">
          <div class="movie__slider">
            <swiper
              :autoplay="{
                delay: 2500,
                disableOnInteraction: false,
              }"
              :effect="'coverflow'"
              :grabCursor="true"
              :centeredSlides="true"
              :slidesPerView="'auto'"
              :initialSlide="5"
              :coverflowEffect="{
                rotate: 50,
                stretch: 0,
                depth: 100,
                modifier: 1,
                slideShadows: true,
              }"
              :pagination="true"
              :modules="modules"
              class="mySwiper"
            >
              <swiper-slide v-for="slider in sliders" :key="slider.id">
                <div class="item">
                  <a :href="`https://image.tmdb.org/t/p/w500/${slider.id}`">
                    <img
                      :src="`https://image.tmdb.org/t/p/w500/${slider.poster_path}`"
                      :alt="slider.title"
                    />
                  </a>
                </div>
              </swiper-slide>
            </swiper>
          </div>
          <!-- movie__slider -->

          <div class="movie__search">
            <div class="container">
              <form @submit.prevent="SearchMovies()">
                <input
                  type="search"
                  id="search"
                  placeholder="검색하세요"
                  v-model="search"
                />
                <button type="submit">검색</button>
              </form>
            </div>
          </div>
          <!-- movie__search -->

          <div class="movie__movies">
            <div class="container">
              <div class="movie__list">
                <ul>
                  <li v-for="movie in movies" :key="movie.id">
                    <a :href="`https://image.tmdb.org/t/p/w500/${movie.id}`">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
                        :alt="movie.title"
                      />
                      <em>
                        <span className="title">{{ movie.title }}</span>
                        <span className="star">{{ movie.vote_average }}</span>
                      </em>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
          </div>
          <!-- movie__movies -->
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<!-- <script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";

import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
import { Autoplay, EffectCoverflow, Pagination } from "swiper";

export default {
  components: {
    Swiper,
    SwiperSlide,
    HeaderCont,
    TitleCont,
    ContactCont,
    FooterCont,
  },
  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref("marvel");

    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=f89466761449b5afaef84a8fb3c666f9&query=${search.value}`
      )
        .then((response) => response.json())
        .then((result) => {
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log(error));
    };
    SearchMovies();

    const TopMovies = () => {
      fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=f89466761449b5afaef84a8fb3c666f9&language=ko-KR`
      )
        .then((response) => response.json())
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log(error));
    };

    TopMovies();
    return {
      modules: [Autoplay, EffectCoverflow, Pagination],
      movies,
      sliders,
      search,
      TopMovies,
      SearchMovies,
    };
  },
};
</script> -->
<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/effect-coverflow";
import "swiper/css/pagination";
import { EffectCoverflow, Pagination, Autoplay } from "swiper";

export default {
  components: {
    Swiper,
    SwiperSlide,
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },
  setup() {
    const movies = ref([]);
    const sliders = ref([]);
    const search = ref(["마블"]);

    const SearchMovies = async () => {
      await fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=f89466761449b5afaef84a8fb3c666f9&query=${search.value}`
      )
        .then((response) => response.json())
        // .then((result) => console.log(result.results))
        .then((result) => {
          movies.value = result.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
    };
    SearchMovies();
    const TopMovies = () => {
      fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=f89466761449b5afaef84a8fb3c666f9&language=ko-KR`
      )
        .then((response) => response.json())
        // .then((result) => console.log(result.results))
        .then((result) => (sliders.value = result.results))
        .catch((error) => console.log("error", error));
    };
    SearchMovies();
    TopMovies();
    return {
      modules: [EffectCoverflow, Pagination, Autoplay],
      movies,
      sliders,
      search,
      SearchMovies,
      TopMovies,
    };
  },
};
</script>

<style lang="scss">
.movie__list {
  ul {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    li {
      width: 19%;
      margin-bottom: 2%;
      position: relative;
      em {
        display: block;
        height: 80px;
        margin-bottom: 30px;
        font-family: var(--font-kor2);
      }
      .title {
        padding: 5px 0;
        display: inline-block;
      }
      .star {
        background: #fff;
        color: #000;
        position: absolute;
        left: 10px;
        top: 10px;
        width: 30px;
        height: 30px;
        border-radius: 100px;
        text-align: center;
        line-height: 30px;
        font-weight: 800;
      }
    }
  }
}
.movie__search {
  margin-bottom: 100px;

  .container {
    position: relative;
  }

  h2 {
    color: var(--white);
    font-size: 40px;
    text-indent: -9999px;
    height: 0;
  }
  input {
    background: var(--bg-light-border);
    border: 1px solid var(--bg-light-border);
    border-radius: 50px;
    color: #000;
    width: 100%;
    padding: 14px 30px;
    font-family: var(--font-kor2);
  }
  button {
    position: absolute;
    right: 6px;
    top: 5px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 0;
    font-family: var(--font-kor2);
    cursor: pointer;
    z-index: 1000;
  }
}

.swiper {
  width: 100%;
  padding-top: 50px;
  padding-bottom: 50px;
}

.swiper-slide {
  background-position: center;
  background-size: cover;
  width: 300px;
}

.swiper-slide img {
  display: block;
  width: 100%;
}
</style>
