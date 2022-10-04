<template>
  <div>
    <Survey :survey="survey" id="surveyContainer" />
    <div v-if="isSurveyCompleted">
      <p>Result</p>
      <code style="white-space:pre;">
        {{surveyResults}}
      </code>
    </div>
  </div>
</template>

<script>
import 'survey-core/defaultV2.min.css';
import { StylesManager, Model } from 'survey-core';
import { Survey } from 'survey-vue-ui';

StylesManager.applyTheme("defaultV2");

const surveyJson = {
  pages: [{
    elements: [{
      type: "html",
      html: "<h1>2023년도 재보궐선거</h1><h2>나에게 가장 적합한 후보자는?</h2>"
    }]
  }, {
    elements: [{
      name: "economy-score",
      title: "경제 부문 질문입니다.",
      type: "radiogroup",
      choices: [
        { value: 5, text: "경제성장 둔화돼도 복지예산 대폭 늘려야" },
        { value: 4, text: "현 경제 수준 고려할때 복지예산 늘려야" },
        { value: 3, text: "현 경제수준 고려할 때 복지예산 줄여야" },
        { value: 2, text: "성장 위해 불필요 복지예싼 대폭 줄여야" },
        { value: 1, text: "잘 모르겠다" }
      ],
      isRequired: true
    }]
  }, 
  {
    elements: [{
      name: "welfare-score",
      title: "외교 안보 부문 질문입니다.",
      type: "radiogroup",
      choices: [
        { value: 5, text: "하이" },
        { value: 4, text: "하이" },
        { value: 3, text: "하이" },
        { value: 2, text: "하이" },
        { value: 1, text: "하이" }
      ],
      isRequired: true
    }]
  },
  {
    elements: [{
      name: "what-would-make-you-more-satisfied",
      title: "What can we do to make your experience more satisfying?",
      type: "comment",
      visibleIf: "{satisfaction-score} = 4"
    }, {
      name: "nps-score",
      title: "On a scale of zero to ten, how likely are you to recommend our product to a friend or colleague?",
      type: "rating",
      rateMin: 0,
      rateMax: 10,
    }],
    visibleIf: "{satisfaction-score} >= 4"
  }, {
    elements: [{
      name: "how-can-we-improve",
      title: "In your opinion, how could we improve our product?",
      type: "comment"
    }],
    visibleIf: "{satisfaction-score} = 3"
  }, {
    elements: [{
      name: "disappointing-experience",
      title: "Please let us know why you had such a disappointing experience with our product",
      type: "comment"
    }],
    visibleIf: "{satisfaction-score} =< 2"
  }],
  showQuestionNumbers: "off",
  pageNextText: "Forward",
  completeText: "Submit",
  showPrevButton: false,
  firstPageIsStarted: true,
  startSurveyText: "Take the Survey",
  completedHtml: "Thank you for your feedback!",
  showPreviewBeforeComplete: "showAnsweredQuestions"
};

export default {
  name: 'MultiPageSurvey',
  components: {
    Survey
  },
  data() {
    const survey = new Model(surveyJson);
    survey.onComplete.add(this.displayResults);

    return {
      survey,
      surveyResults: "",
      isSurveyCompleted: false 
    }
  },
  methods: {
    displayResults (sender) {
      this.surveyResults = JSON.stringify(sender.data, null, 4);
      this.isSurveyCompleted = true;
    }
  },
}
</script>
<style>

</style>