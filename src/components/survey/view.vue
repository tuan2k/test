<template>
    <div>
        <div id="home">
            <router-link to="/survey/list"><h4 class="text-primary">List Survey</h4></router-link>
            <div id="surveyResult"></div>
            <div class="space"></div>
        </div>
    </div>
</template>
<script>
import "survey-vue/modern.min.css";
import {Survey,StylesManager, Model } from "survey-vue"

StylesManager.applyTheme("modern");
let surveyJson = {
 "pages": [
  {
   "name": "Trang 1",
   "elements": [
    {
     "type": "text",
     "name": "question1",
     "title": "Bạn tên là gì?",
     "isRequired": true
    },
    {
     "type": "checkbox",
     "name": "question2",
     "title": "Ai là người đẹp trai nhất?",
     "isRequired": true,
     "choices": [
      "item1",
      "item2",
      "item3"
     ]
    },
    {
     "type": "radiogroup",
     "name": "question3",
     "title": "Bạn có bao nhiêu người yêu!!!",
     "isRequired": true,
     "choices": [
      "item1",
      "item2",
      "item3"
     ]
    }
   ]
  },
  {
   "name": "Trang 2",
   "elements": [
    {
     "type": "text",
     "name": "question4",
     "title": "Bạn là ai hả?",
     "isRequired": true
    },
    {
     "type": "checkbox",
     "name": "question5",
     "title": "Bạn có những gì?",
     "isRequired": true,
     "choices": [
      "item1",
      "item2",
      "item3"
     ]
    },
    {
     "type": "comment",
     "name": "question6",
     "title": "Tại sao bạn ghét tôi?",
     "isRequired": true
    }
   ]
  }
 ]
}



export default {
  name: 'doSurvey',
  components: {
    Survey,                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
  },
  created(){
      this.resultSurvey = this.$route.params.survey;
      this.question = this.$route.params.question;
  },
  data() {
    const survey = new Model(surveyJson);
    survey.focusFirstQuestionAutomatic = false;
    survey.onComplete.add(this.alertResults);
    survey.data = {"question1":"NGUYEN THANH TUAN","question2":["item1"],"question3":"item1","question4":"TOI LA TOI","question5":["item1","item3"],"question6":"ALOOO"}
    // calfunctionl  save data into IPFS
    return {
        survey,
        resultSurvey: [],
        question: {},
        result : {}
    };
  },
  mounted() {
    var survey = new Model(this.question);
    var surveyResultNode = document.getElementById("surveyResult");
    surveyResultNode.innerHTML = "";
    var surveyAnalyticsTabulator = new SurveyAnalyticsTabulator.Tabulator(survey,this.resultSurvey);
    surveyAnalyticsTabulator.render(surveyResultNode);
  },
  methods: {
  },
}
</script>
<style scoped>
#home {
  margin-left: 50px;
  margin-right: 50px;
}
.space {
    margin-bottom: 50px;
}
</style>