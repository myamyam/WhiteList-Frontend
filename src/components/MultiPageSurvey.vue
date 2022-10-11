<template>
  <div>
    <Survey :survey="survey" id="surveyContainer" />
    <div v-if="isSurveyCompleted">
      <p>Result</p>
      <code style="white-space: pre">
        {{ surveyResults }}
      </code>
    </div>
  </div>
</template>

<script>
import "survey-core/defaultV2.min.css";
import { StylesManager, Model } from "survey-core";
import { Survey } from "survey-vue-ui";

StylesManager.applyTheme("defaultV2");

const surveyJson = {
  pages: [
    {
      elements: [
        {
          type: "html",
          html: "<h1>2023년도 재보궐선거</h1><h2>나에게 가장 적합한 후보자는?</h2>",
        },
      ],
    },
    {
      elements: [
        {
          name: "question1",
          title:
            "광주광역시 청소년에게 가장 도움이 될 것 같은체험형 교육 방안을 선택해주세요",
          type: "radiogroup",
          choices: [
            {
              value: "Chung",
              text: "문화체험카드 지원 / 마을동아리, 청소년 자치학교, 마을교육공동체 행정협의회 운영",
            },
            {
              value: "Jang",
              text: "동서양 고전 교육과 독서교육 활성화 / 최소 15시간 단위의 진로체험 활동 실시 ",
            },
            {
              value: "Kang",
              text: "직업체험 기관(KIDZANIA) 광주 유치 / 학생 자치 활동 및 동아리 활성화",
            },
            {
              value: "Lee",
              text: "365 디지털 교육 복합문화 공간 구축 / 글로벌 융복합 봉사센터 건립, 스포츠*예능 클럽 활성화",
            },
          ],
          isRequired: true,
        },
      ],
    },
    {
      elements: [
        {
          name: "question2",
          title:
            "광주광역시 청소년의 안전을 확보하기 위한 가장 좋은 방안을 선택해주세요",
          type: "radiogroup",
          choices: [
            { value: "Jang", text: "학교폭력 전담 지도 기관 및 정책 신설" },
            {
              value: "Lee",
              text: "학생 건강체력 평가를 통해 저 체력 학생 특별 관리 / 친환경 급식 / 통학버스 무료 지원",
            },
            { value: "Chung", text: "365 녹색안전행복망 구축" },
          ],
          isRequired: true,
        },
      ],
    },
    {
      elements: [
        {
          name: "question3",
          title:
            "광주광역시의 보육 환경을 가장 효과적으로 개선할 방안을 선택해주세요",
          type: "radiogroup",
          choices: [
            {
              value: "Jang",
              text: "방학 중 유치원 방과후 과정 / 돌봄교실에 무상급식 지원",
            },
            {
              value: "Lee",
              text: "공사립 유치원 평등지원, 유치원 무상급식, 무상교육",
            },
            {
              value: "Kang",
              text: "영유아,어린이 보육과 교육 통합지원시스템 구축",
            },
            { value: "Chung", text: "희망하는 모든 학생 야간돌봄 실시" },
          ],
          isRequired: true,
        },
      ],
    },
    {
      elements: [
        {
          name: "question4",
          title: "광주광역시의 지역 특색을 잘 살리는 교육 방안을 선택해주세요",
          type: "radiogroup",
          choices: [
            {
              value: "Chung",
              text: " 5.18 온라인 콘텐츠 개발 보급 / 학교로 찾아가는 교육 및 체험학습 확대",
            },
            {
              value: "Ok",
              text: "지역사회 거버넌스 네트워크 구축 / 365 디지털 교육복합문화 공간 구축",
            },
            {
              value: "Kang",
              text: "학교 밖 마을 축제 / 지역연계형 학교 공연단 활동 지원 ",
            },
            {
              value: "Lee",
              text: " '광주교육시민협치진흥원' 신설 / '광주온마을학교' 운영",
            },
            {
              value: "Jang",
              text: "교육역사박물관 신설로 광주 역사 바르게 알기 / 이념논리 탈피와 시대 정신이 있는 교육 본질 충실",
            },
          ],
          isRequired: true,
        },
      ],
    },
  ],
  showQuestionNumbers: "on",
  pageNextText: "Forward",
  completeText: "Submit",
  showPrevButton: true,
  firstPageIsStarted: true,
  startSurveyText: "Take the Survey",
  completedHtml: "Thank you for your feedback!",
  showPreviewBeforeComplete: "showAnsweredQuestions",
};

export default {
  name: "MultiPageSurvey",
  components: {
    Survey,
  },
  data() {
    const survey = new Model(surveyJson);
    survey.onComplete.add(this.displayResults);

    return {
      survey,
      surveyResults: "",
      isSurveyCompleted: false,
    };
  },
  methods: {
    displayResults(sender) {
      this.surveyResults = JSON.stringify(sender.data, null, 4);
      this.isSurveyCompleted = true;
    },
  },
};
</script>
<style>
#surveyElement {
  --primary: #1ab7fa;
  --primary-light: rgba(26, 183, 250, 0.1);
  --secondary: #1ab7fa;
  --background: #555555;
  --background-dim: #4d4d4d;
  --background-dim-light: #4d4d4d;
  --foreground: #ededed;
}
</style>
