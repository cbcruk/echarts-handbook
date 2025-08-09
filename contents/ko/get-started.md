# 시작하기

## Apache ECharts 설치하기

Apache ECharts는 여러 다운로드 방법을 지원하며, 이는 다음 튜토리얼 [설치](${lang}/basics/download)에서 자세히 설명됩니다. 여기서는 [jsDelivr](https://www.jsdelivr.com/package/npm/echarts) CDN을 통해 빠르게 설치하는 방법을 예시로 설명하겠습니다.

[https://www.jsdelivr.com/package/npm/echarts](https://www.jsdelivr.com/package/npm/echarts)에서 `dist/echarts.js`를 선택하고, 클릭한 후 `echarts.js` 파일로 저장하세요.

> 이러한 파일들에 대한 자세한 정보는 다음 튜토리얼 [설치](${lang}/basics/download)에서 확인할 수 있습니다.

## ECharts 포함하기

방금 저장한 `echarts.js`가 있는 디렉토리에 다음 내용으로 새 `index.html` 파일을 생성하세요:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <!-- 방금 다운로드한 ECharts 파일을 포함합니다 -->
    <script src="echarts.js"></script>
  </head>
</html>
```

이 `index.html`을 열면 빈 페이지가 표시됩니다. 하지만 걱정하지 마세요. 콘솔을 열어서 오류 메시지가 없는지 확인한 후 다음 단계로 진행할 수 있습니다.

## 간단한 차트 그리기

그리기 전에 정의된 높이와 너비를 가진 ECharts용 DOM 컨테이너를 준비해야 합니다. 앞서 소개한 `</head>` 태그 뒤에 다음 코드를 추가하세요.

```html
<body>
  <!-- ECharts를 위한 정의된 너비와 높이를 가진 DOM을 준비합니다 -->
  <div id="main" style="width: 600px;height:400px;"></div>
</body>
```

그런 다음 [echarts.init](${mainSitePath}api.html#echarts.init) 메서드로 echarts 인스턴스를 초기화하고 [setOption](${mainSitePath}api.html#echartsInstance.setOption) 메서드로 echarts 인스턴스를 설정하여 간단한 막대 차트를 생성할 수 있습니다. 다음은 완전한 코드입니다.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>ECharts</title>
    <!-- 방금 다운로드한 ECharts 파일을 포함합니다 -->
    <script src="echarts.js"></script>
  </head>
  <body>
    <!-- ECharts를 위한 정의된 너비와 높이를 가진 DOM을 준비합니다 -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
      // 준비된 dom을 기반으로 echarts 인스턴스를 초기화합니다
      var myChart = echarts.init(document.getElementById('main'));

      // 차트의 구성 항목과 데이터를 지정합니다
      var option = {
        title: {
          text: 'ECharts 시작하기 예제'
        },
        tooltip: {},
        legend: {
          data: ['판매량']
        },
        xAxis: {
          data: ['셔츠', '카디건', '시폰', '바지', '하이힐', '양말']
        },
        yAxis: {},
        series: [
          {
            name: '판매량',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
          }
        ]
      };

      // 방금 지정한 구성 항목과 데이터를 사용하여 차트를 표시합니다.
      myChart.setOption(option);
    </script>
  </body>
</html>
```

이것이 Apache ECharts로 만든 첫 번째 차트입니다!

<md-example src="doc-example/getting-started&reset=1&edit=1"></md-example>