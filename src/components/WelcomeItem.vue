<template>
  <div class="about">
    <div class="row gy-2 gx-3 align-items-center mt-5" v-for="(value, index) in weekDay">
      <div class="col-auto" >
        <div class=" ">{{ value }}</div>
      </div>
      <div class="col-auto">
        
        <div class="form-control button r mx-4 my-2" id="button">
          <input type="checkbox" class="form-check-checkbox checkbox" :name="value" :value="value" :id="index" v-model="isSuccess">
            <span class="knobs"></span >
            <span class="layer"></span>
            <label class="form-check-label" :for="index">切換狀態</label>   
        </div>

      </div>
      <div class="col-auto">
        <div class="alert alert-success mt-2" v-if="isSuccess">本日供餐</div>
        <div class="alert alert-danger" v-else="!isSuccess">本日不供餐</div>
      </div>
      <div class="col-auto" >
        <el-time-select
          placeholder="請選擇時間"
          v-model="startTime"
          start="00:00"
          step="00:30"
          end="23:30"
        >
        </el-time-select>
      </div>
      <div class="col-auto">
        <div class=""> - </div>
      </div>
      <div class="col-auto">
        <el-time-select
          placeholder="請選擇時間"
          v-model="endTime"
          start="00:30"
          step="00:30"
          end="23:59"
          :minTime="startTime"
        >
        </el-time-select>
      </div>
    </div> 
    
  </div>
    
</template>

<script>
export default {
  data() {
    return {
      isSuccess: true,
      startTime: '',
      endTime: '',
      weekDay:{
          "week_day0": "星期日",
          "week_day6": "星期一",
          "week_day5": "星期二",
          "week_day4": "星期三",
          "week_day3": "星期四",
          "week_day2": "星期五",
          "week_day1": "星期六",
        },
    }
  },
  mounted() {
     
    },
    methods: {
      toggleCheckAnswer() {
        this.checkAnswer = !this.checkAnswer;

      },
    }
  }
</script>

<style>
button {
  border: none;
}
.button-cover:before {
  counter-increment: button-counter;
  content: counter(button-counter);
  position: absolute;
  right: 0;
  bottom: 0;
  color: #d7e3e3;
  font-size: 12px;
  line-height: 1;
  padding: 5px;
}

.button-cover,
.knobs,
.layer {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

.button {
  position: relative;
  top: 50%;
  width: 74px;
  height: 36px;
  /* margin: -20px auto 0 auto; */
  overflow: hidden;
}

.button.r,
.button.r .layer {
  border-radius: 100px;
}

.button.b2 {
  border-radius: 2px;
}

.checkbox {
  position: relative;
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  opacity: 0;
  cursor: pointer;
  z-index: 3;
}

.knobs {
  z-index: 2;
}

.layer {
  width: 100%;
  background-color: #6c757d;
  transition: 0.3s ease all;
  z-index: 1;
}

/* Button*/
#button .knobs:before {
  content: "X";
  position: absolute;
  top: 3px;
  left: 4px;
  width: 30px;
  height: 30px;
  color: #6c757d;
  font-size: 10px;
  font-weight: bold;
  text-align: center;
  line-height: 1;
  padding: 9px 4px;
  background-color: #fff;
  border-radius: 50%;
  transition: 0.3s cubic-bezier(0.18, 0.89, 0.35, 1.15) all;
}

#button .checkbox:checked + .knobs:before {
  content: "✓";
  left: 42px;
  color: #20c997;
  background-color: #fff;
}

#button .checkbox:checked ~ .layer {
  background-color: #20c997;
}

#button .knobs,
#button .knobs:before,
#button .layer {
  transition: 0.3s ease all;
}
</style>