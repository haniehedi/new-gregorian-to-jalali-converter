USE it in vueCli :  <br>
 this is a datepicker, works with gregorian date but shows jalali 
 
-------------
install : 

npm install --save new-gregorian-to-jalali-converter <br>
-------------------------------
in main.js : 

import Vue from "vue"; <br>
import newGregorianToJalaliConverter from 'new-gregorian-to-jalali-converter';  <br>
Vue.use(newGregorianToJalaliConverter); <br>
--------------------------------
the tag is : 

newGregorianToJalaliConverter  v-model="todayGr"  :emitGrValue="emitGrValue"
--------------------------------

