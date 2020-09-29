<template>
  <date-picker :value="prValue" @input="onValueChanged"></date-picker>
</template>

<script>
import VuePersianDatetimePicker from "vue-persian-datetime-picker";
import moment from "moment-jalaali";

const jalaliToGregorian = (prdate) =>
  moment(prdate, "jYYYY/jM/jD").format("YYYY/MM/DD");

const toEnglishDigits = (str) => {
  var persianNumbers = [
      /۰/g,
      /۱/g,
      /۲/g,
      /۳/g,
      /۴/g,
      /۵/g,
      /۶/g,
      /۷/g,
      /۸/g,
      /۹/g,
    ],
    arabicNumbers = [
      /۰/g,
      /۱/g,
      /۲/g,
      /۳/g,
      /۴/g,
      /۵/g,
      /۶/g,
      /۷/g,
      /۸/g,
      /۹/g,
    ],
    fixNumbers = function (str) {
      if (typeof str === "string") {
        for (var i = 0; i < 10; i++) {
          str = str.replace(persianNumbers[i], i).replace(arabicNumbers[i], i);
        }
      }
      return str;
    };
  return fixNumbers(str);
};

const convertJalaliToGregorian = (shamsiDate) => {
  let grDateStr = jalaliToGregorian(toEnglishDigits(shamsiDate));
  grDateStr = toEnglishDigits(grDateStr);
  const grDate = new Date(grDateStr);
  return grDate;
};

const convertGregorianToJalali = (grDate) => {
  return moment(grDate).format("jYYYY/jMM/jDD");
};

export default {
  components: {
    datePicker: VuePersianDatetimePicker,
  },
  props: ["value", "emitGrValue"],

  computed: {
    prValue() {
      if (this.emitGrValue == false) {
        const prval = moment(this.value, "jYYYY/jM/jD").Date;
        return prval;
      } else {
        const prval = convertGregorianToJalali(this.value);
        return prval;
      }
    },
  },
  methods: {
    onValueChanged(currentValue) {
      if (this.emitGrValue) {
        const grDate = convertJalaliToGregorian(currentValue);
        this.$emit("input", grDate);
      } else {
        this.$emit("input", currentValue);
      }
    },
  },
};
</script>

<style>
</style>