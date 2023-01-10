<template>
  <div class='template'>
    <h1 class='title'>벌써 12시~</h1>
    <h2 class='sub-title'>찐 판교 직장인이 추천하는 맛집 리스트</h2>
    <div class='filter-wrapper'>
      <ul class='filter-list'>
        <li v-for='filter in filters' :key='filter.id' :class='{ active: filter.id === selectedFilter }' class='filter'>
          <button
            type='button' class='button' :class='{active: filter.id === selectedFilter }'
            @click='changeFilter(filter.id)'>
            {{ filter.name }}
          </button>
        </li>
      </ul>
      <ul class='sub-filter-list'>
        <!--         TODO: Add 전체 after create component -->
        <!--        <li class='sub-filter'>전체</li>-->
        <li v-for='subFilter in currentSubFilters' :key='subFilter.id' class='sub-filter'>
          <input
            :id='subFilter.id'
            v-model='selectedSubFilters'
            type='checkbox'
            aria-hidden='true'
            :value='subFilter' />
          <label :for='subFilter.id'>
            {{ subFilter.name }}
          </label>
        </li>
      </ul>
      <div class='filter-condition-wrapper'>
        <p class='filter-title'>필터조건</p>
        <ul class='filter-condition-list'>
          <li v-for='selectedSubFilter in selectedSubFilters' :key='selectedSubFilter.id' class='filter-condition'>
            <button type='button' class='button' @click='deleteFilter(selectedSubFilter.id)'>
              {{ selectedSubFilter.name }}
              <FontAwesomeIcon icon='fa-circle-xmark' />
            </button>
          </li>
        </ul>
      </div>
    </div>
    <div class='search-list-wrapper'>
      <ul class='search-list'>
        <li v-for='(data) in dataList' :key='data.id'>
          <!--           TODO: 나중에~ -->
          <!--          <div v-if='index <= 3' class='grade-mark'>-->
          <!--            <span>{{ index }}위</span>-->
          <!--          </div>-->
          <div class='store-info-wrapper'>
            <div class='image-wrapper'>
              <div class='main-image-wrapper'>
                <img class='main-image' :src='data.imageUrl' :alt='`${data.name} 이미지`' />
              </div>
              <ul v-if='data.subImageUrls.length' class='sub-image-list'>
                <li v-for='(subImageUrl, index) in data.subImageUrls.slice(0, 3)' :key='subImageUrl + index'>
                  <img :src='subImageUrl' alt='추가 이미지'>
                </li>
              </ul>
            </div>
            <div class='store-info'>
              <div class='store-main-info'>
                <span class='name'>{{ data.name }}</span>
                <span class='type'>{{ data.type.join(',') }}</span>
              </div>
              <div v-if='data.openTime || data.closeTime' class='time-wrapper'>
                <span class='open-time'>{{ data.openTime || '미정' }}</span>
                ~
                <span class='close-time'>{{ data.closeTime || '미정' }}</span>
              </div>
              <ul class='star-group-list form-group'>
                <li class='star-group'>
                  <span class='star-title'>맛</span>
                  <FontAwesomeIcon icon='fa-solid fa-star' />
                  <span class='star-rate'><b>{{ data.star }}</b></span>
                </li>
                <li class='star-group'>
                  <span class='star-title'>가성비</span>
                  <FontAwesomeIcon icon='fa-solid fa-star' />
                  <span class='star-rate'>{{ data.priceStar }}</span>
                </li>
              </ul>
              <div v-if='data.recommendMenus.length' class='form-group'>
                <span class='tip-label'>
                  <FontAwesomeIcon icon='fa-regular fa-thumbs-up' />
                  추천메뉴
                </span>
                <ul class='recommend-menu-list'>
                  <li v-for='recommendMenu in data.recommendMenus' :key='recommendMenu' class='recommend-menu'>
                    {{ recommendMenu }}
                  </li>
                </ul>
              </div>
              <div v-if='data.mdReview' class='form-group md-review'>
                <span class='tip-label'>
                  <FontAwesomeIcon icon='fa-regular fa-comment-dots' />
                  MD평
                </span>
                <p class='tip'>{{ data.mdReview }}</p>
              </div>
              <div v-if='data.reserveTip' class='form-group tip-reserve'>
                <span class='tip-label'>
                  <FontAwesomeIcon icon='fa-pen-to-square' />
                  예약팁
                </span>
                <p class='tip'>{{ data.reserveTip }}</p>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue'

type Filters = 'building' | 'price' | 'type' | 'star';

type SubFilter = {
  id: string;
  name: string;
};

const filters = [
  {
    id: 'building',
    name: '건물',
    subFilters: [
      {
        id: 'hyundai-department',
        name: '현대백화점'
      },
      { id: 'avenue-france', name: '아브뉴프랑' }
    ]
  },
  {
    id: 'price', name: '가격대',
    subFilters: [
      { id: 'under-10000', name: '~ 10,000원' },
      { id: 'under-20000', name: '~ 20,000원' },
      { id: 'under-30000', name: '~ 30,000원' },
      { id: 'under-40000', name: '~ 40,000원' },
      { id: 'under-50000', name: '~ 50,000원' },
      { id: 'over-50000', name: '50,000원 이상' }
    ]
  },
  { id: 'type', name: '종류' },
  { id: 'star', name: '평점' }
]

const dataList = [
  {
    id: 'jungdon',
    name: '정돈',
    type: ['일식', '돈까스'],
    openTime: '10:30',
    closeTime: '20:00',
    imageUrl: 'https://via.placeholder.com/200',
    subImageUrls: ['https://via.placeholder.com/50', 'https://via.placeholder.com/50', 'https://via.placeholder.com/50', 'https://via.placeholder.com/50'],
    star: 5,
    priceStar: 4,
    recommendMenus: ['안심', '안심+새우'],
    mdReview: '안심 꼭 드셔보세요. 양이 적어보이지만 매우 든든합니다. 새우튀김도 맛있어서 새우+안심 세트도 추천합니다!',
    reserveTip: '현대식품관 앱에서 예약하실 수 있습니다. 5분만에 대기인원 3~4팀 정도 빠집니다.'
  }
]

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      dataList,
      filters,
      selectedFilter: 'building',
      selectedSubFilters: [] as unknown as SubFilter[]
    }
  },
  computed: {
    currentSubFilters(): SubFilter[] {
      return filters.find(f => f.id === this.selectedFilter)?.subFilters || []
    }
  },
  methods: {
    changeFilter(type: Filters) {
      this.selectedFilter = type
    },
    deleteFilter(id: string) {
      this.selectedSubFilters = this.selectedSubFilters.filter(f => f.id !== id)
    }
  }
})
</script>

<style lang='scss'>
$max-width: 960px;

@mixin form-width {
  max-width: $max-width;
  margin: 0 auto;
}

ul, li {
  list-style: none;
  padding: 0;
  margin: 0;
}

p {
  margin: 0;
}

.title,
.sub-title,
.filter-wrapper,
.search-list-wrapper {
  @include form-width;
}

.title,
.sub-title {
  text-align: center;
}

.title {
  padding-top: 4rem;
}

.sub-title {
  font-size: .9rem;
  margin-top: 1rem;
}

.filter-list {
  display: flex;
  justify-content: center;
  padding: 0 1rem;
  margin-top: 3.4rem;

  .filter {
    margin-right: 2rem;

    &:last-child {
      margin-right: 0;
    }
  }

  .button {
    border: none;
    padding: 0.5rem;
    background-color: transparent;
    cursor: pointer;

    &.active {
      font-weight: bold;
      border-bottom: 2px solid;
    }
  }
}

.sub-filter-list {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;

  .sub-filter {
    display: flex;
    align-items: center;
    margin-right: 2.5rem;

    input[type=checkbox] {
      opacity: 0;
      position: absolute;
      cursor: pointer;
    }

    label {
      display: flex;
      align-items: center;
      font-size: .8rem;
      cursor: pointer;

      &:before {
        display: inline-block;
        content: '';
        font-size: .6rem;
        width: 1.2rem;
        height: 1.2rem;
        border-radius: .6rem;
        margin-right: .5rem;
        border: 1px solid;
        transition: background-color .3s ease-out;
      }

      :after {
        font-size: .6rem;
      }
    }

    input[type=checkbox]:checked ~ label:before {
      content: '\002714';
      color: #fff;
      background-color: #58CC5C;
      border-color: #58CC5C;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background-color .3s ease-out, border-color .3s ease-out;
    }
  }
}

.filter-condition-wrapper {
  display: flex;
  align-items: center;
  padding: 0.8rem 1rem;
  border: 1px solid #eee;
  border-radius: .3rem;

  .filter-title {
    font-weight: bold;
    margin-right: 2rem;
  }

  .filter-condition-list {
    .filter-condition {
      display: inline-block;
      margin-right: .7rem;

      &:last-child {
        margin-right: 0;
      }
    }

    .button {
      cursor: pointer;
      font-size: 0.9rem;
      color: #fff;
      font-size: .8rem;
      border: none;
      background-color: #58CC5C;
      border-radius: 2rem;
      padding: 0.5rem 0.6rem 0.4rem;
    }
  }
}

.search-list-wrapper {
  border: 1px solid #eee;
  border-radius: .3rem;
  margin-top: .5rem;

  .form-group {
    margin-top: 1.3rem;
  }

  .search-list {
    padding: 1.5rem 1rem;
  }

  .store-info-wrapper {
    display: grid;
    grid-template-columns: 10rem 1fr;
    grid-column-gap: 1rem;

    .image-wrapper {
      display: flex;
      flex-direction: column;

      .main-image-wrapper {
        width: 10rem;
        height: 10rem;
        background-color: #eee;
      }

      .main-image {
        width: inherit;
        height: inherit;
        object-fit: fill;
      }

      .sub-image-list {
        display: flex;
        flex-wrap: wrap;
        grid-column-gap: 0.3rem;
        margin-top: 0.3rem;

        .sub-image {
          background-color: #eee;
        }
      }
    }

    .store-info {
      .store-main-info {
        display: flex;
        align-items: center;
      }

      .name {
        font-size: 1.3rem;
        font-weight: bold;
        margin-right: .5rem;
      }

      .type {
        font-size: .9rem;
        color: #9a9a9a;
      }

      .star-group-list {
        display: flex;
        align-items: center;

        .star-group {
          display: flex;
          align-items: center;

          &:not(:last-child):after {
            content: '';
            width: 2px;
            height: 2px;
            background-color: #aaa;
            margin: 0 .6rem;
            display: inline-block;
          }
        }

        .fa-star {
          color: #ec493f;
          margin-right: .2rem;
          margin-left: .5rem;
          margin-top: -1px;
        }

        .star-rate {
          font-weight: bold;
          margin-top: 1px;
        }
      }

      .tip-label {
        display: inline-block;
        border-radius: .3rem;
        font-weight: bold;
        font-size: .8rem;
      }

      .tip {
        margin-top: .5rem;
        color: #666;
      }

      .recommend-menu-list {
        margin-top: .5rem;

        .recommend-menu {
          display: inline-block;
          margin-right: .5rem;
          font-size: .8rem;
          background-color: #d5eafd;
          color: #3298f3;
          padding: .3rem .5rem;
          border-radius: 1rem;

          &:last-child {
            margin-right: 0;
          }
        ;
        }
      }
    }
  }
}
</style>
