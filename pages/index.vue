<template>
  <div class='template'>
    <h1>벌써 12시~</h1>
    <h2>찐 판교 직장인이 추천하는 맛집 리스트</h2>
    <div class='filter-wrapper'>
      <ul class='filter-list'>
        <li v-for='filter in filters' :key='filter.id' :class='{ active: filter.id === selectedFilter }'>
          <button type='button' @click='changeFilter(filter.id)'>
            {{ filter.name }}
          </button>
        </li>
      </ul>
      <ul class='filter-sub-list'>
        <li>전체</li>
        <li v-for='subFilter in currentSubFilters' :key='subFilter.id'>
          <input type='checkbox' :id='subFilter.id' v-model='selectedSubFilters' :value='subFilter' />
          <label :for='subFilter.id' class='12-checkbox'>
            {{ subFilter.name }}
          </label>
        </li>
      </ul>
      <div class='filter-condition-wrapper'>
        <p>필터조건</p>
        <ul class='filter-condition-list'>
          <li v-for='selectedSubFilter in selectedSubFilters' :key='selectedSubFilter.id'>
            {{ selectedSubFilter.name }}
          </li>
          <!--          <li class='filter-condition-start'>-->
          <!--            <button type='button'>-->
          <!--              4점 이상-->
          <!--              <span class='remove-icon'>x</span>-->
          <!--            </button>-->
          <!--          </li>-->
          <!--          <li class='filter-condition-price'>-->
          <!--            <button type='button'>-->
          <!--              ~15,000원-->
          <!--              <span class='remove-icon'>x</span>-->
          <!--            </button>-->
          <!--          </li>-->
        </ul>
      </div>
    </div>
    <div class='search-list-wrapper'>
      <ul class='search-list'>
        <li v-for='(data, index) in dataList' :key='data.id'>
          <div v-if='index <= 3' class='grade-mark'>
            <span>{{ index }}위</span>
          </div>
          <div class='store-info'>
            <div class='image-wrapper'>
              <img :src='data.imageUrl' :alt='`${data.name} 이미지`' />
            </div>
            <div>
              <span class='name'>{{ data.name }}</span>
              <span class='type'>{{ data.type.join(',') }}</span>
            </div>
            <div class='star'>
              <ul class='start-list'>
                <li v-for='(num, index) in 5' :key='num' class='star' :class='{filled: index < data.star }'>
                  star
                </li>
              </ul>
            </div>
            <div v-if='data.mdReview' class='tip md-review'>
              <span>MD 평</span>
              <p>{{ data.mdReview }}</p>
            </div>
            <div v-if='data.reserveTip' class='tip tip-reserve'>
              <span>예약팁</span>
              <p>{{ data.reserveTip }}</p>
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

type SubFilterGroup = {
  id: string;
  name: string;
}[];

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
    imageUrl: '',
    star: 3,
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
      selectedSubFilters: []
    }
  },
  methods: {
    changeFilter(type: Filters) {
      this.selectedFilter = type
    }
  },
  computed: {
    currentSubFilters(): SubFilterGroup {
      return filters.find(f => f.id === this.selectedFilter)?.subFilters || []
    }
  }
})
</script>
