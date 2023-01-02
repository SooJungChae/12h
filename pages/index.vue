<template>
  <div class='template'>
    <h1>벌써 12시~</h1>
    <h2>찐 판교 직장인이 추천하는 맛집 리스트</h2>
    <div class='filter-wrapper'>
      <ul class='filter-list'>
        <li>건물</li>
        <li>가격대</li>
        <li>종류</li>
        <li>평점</li>
      </ul>
      <ul class='filter-sub-list'>
        <li>전체</li>
        <li>현대백화점</li>
        <li>아브뉴프랑</li>
      </ul>
      <div class='filter-condition-wrapper'>
        <p>필터조건</p>
        <ul class='filter-condition-list'>
          <li class='filter-condition-start'>
            <button type='button'>
              4점 이상
              <span class='remove-icon'>x</span>
            </button>
          </li>
          <li class='filter-condition-price'>
            <button type='button'>
              ~15,000원
              <span class='remove-icon'>x</span>
            </button>
          </li>
        </ul>
      </div>
    </div>
    <div class='search-list-wrapper'>
      <ul class='search-list'>
        <li>
          <div class='grade-mark'>
            <span>1위</span>
          </div>
          <div class='store-info'>
            <div class='image-wrapper'>
              <img src='.' alt='temp' />
            </div>
            <a href='#'>
              <span class='name'>정돈</span>
              <span class='type'>일식/돈까스</span>
            </a>
            <div class='star'>
              <ul class='start-list'>
                <li class='star filled'>star</li>
                <li class='star filled'>star</li>
                <li class='star filled'>star</li>
                <li class='star filled'>star</li>
                <li class='star'>star</li>
              </ul>
            </div>
            <div class='tip md-review'>
              <span>MD 평</span>
              <p>안심 꼭 드셔보세요. 양이 적어보이지만 매우 든든합니다. 새우튀김도 맛있어서 새우+안심 세트도 추천합니다!</p>
            </div>
            <div class='tip tip-reserve'>
              <span>예약팁</span>
              <p>현대식품관 앱에서 예약하실 수 있습니다. 5분만에 대기인원 3~4팀 정도 빠집니다.</p>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang='ts'>
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>
