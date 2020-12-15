<template>
  <div class="pages">
    <div>
      <button @click="handleClick()">点击</button>
      <div class="rows">
        <div
          class="row"
          v-for="(cell, index) in cells"
          :key="index"
          :class="['row' + index, isClick ? 'running' : 'paused']"
          :title="cell.id"
        >
          {{cell.number}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isClick: false,
      cells: Array.apply(null, { length: 81 }).map(function (_, index) {
        return {
          id: index,
          number: (index % 9) + 1,
        };
      }),
    };
  },
  mounted() {
    let rows = document.querySelectorAll(".row");
    rows.forEach((item) => {
      item.addEventListener("animationend", function () {
        console.log(item.style);
        item.style.animationName = "";
        console.log(item.style);
      });
    });
  },
  methods: {
    handleClick() {
      this.isClick = !this.isClick;
      this.cells.sort(() => (Math.random() > 0.5 ? -1 : 1));
      this.isClick = true;
      let rows = document.querySelectorAll(".row");
      rows.forEach((item) => {
        console.log(item.className);
        if (item.className.indexOf("row5") > -1) {
          item.style.animationName = "animX";
          item.style.animationDuration = "2s";
          item.style.animationDelay = "0s";
        }
      });
    },
  },
};
</script>

<style>
.pages {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.rows {
  width: 235px;
  height: 235px;
  margin-top: 10px;
  display: flex;
  flex-wrap: wrap;
}

.row {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 25px;
  height: 25px;
  border: 1px solid #aaa;
  margin-right: -1px;
  margin-bottom: -1px;
}

.row5 {
  animation-name: animX;
  animation-duration: 2s;
  animation-delay: 0s;
  animation-play-state: paused;
  
}

@keyframes animX {
  0% {
    transform: translateY(0px);
    transform: translateX(0px);
  }
  50% {
    transform: translate(130px, 130px);
    transition: transform 1s;
  }
  100% {
    transform: translateY(0px);
    transform: translateX(0px);
  }
}
</style>
