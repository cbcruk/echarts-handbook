# NPM 패키지로 ECharts 사용하기

ECharts를 패키지로 사용하는 방법에는 두 가지 접근법이 있습니다. 가장 간단한 방법은 `echarts`에서 가져와서 모든 기능을 즉시 사용할 수 있게 하는 것입니다. 하지만 `echarts/core`와 `echarts/charts`처럼 필요한 부분만 가져와서 번들 크기를 대폭 줄이는 것이 권장됩니다.

## NPM을 통한 ECharts 설치

다음 명령을 사용하여 npm을 통해 ECharts를 설치할 수 있습니다

```shell
npm install echarts
```

## 모든 ECharts 기능 가져오기

ECharts의 모든 기능을 포함하려면 단순히 `echarts`를 가져오면 됩니다.

```js
import * as echarts from 'echarts';

// echarts 인스턴스 생성
var myChart = echarts.init(document.getElementById('main'));

// 차트 그리기
myChart.setOption({
  title: {
    text: 'ECharts 시작하기 예제'
  },
  tooltip: {},
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
});
```

## 번들 크기 줄이기

위 코드는 ECharts의 모든 차트와 컴포넌트를 가져오지만, 모든 컴포넌트를 포함시키고 싶지 않다면 ECharts에서 제공하는 트리 셰이킹 가능한 인터페이스를 사용하여 필요한 컴포넌트만 번들링하고 최소한의 번들을 얻을 수 있습니다.

```js
// echarts 핵심 모듈을 가져오면 echarts 사용에 필요한 인터페이스가 제공됩니다.
import * as echarts from 'echarts/core';

// 막대 차트를 가져오며, 모두 Chart 접미사가 붙습니다
import { BarChart } from 'echarts/charts';

// 제목, 툴팁, 직사각형 좌표계, 데이터셋, 변환 컴포넌트를 가져옵니다
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent
} from 'echarts/components';

// 범용 전환 및 라벨 레이아웃과 같은 기능
import { LabelLayout, UniversalTransition } from 'echarts/features';

// Canvas 렌더러 가져오기
// CanvasRenderer 또는 SVGRenderer를 포함하는 것은 필수 단계입니다
import { CanvasRenderer } from 'echarts/renderers';

// 필요한 컴포넌트 등록
echarts.use([
  BarChart,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  LabelLayout,
  UniversalTransition,
  CanvasRenderer
]);

// 차트는 이전과 동일한 방식으로 초기화되고 구성됩니다
var myChart = echarts.init(document.getElementById('main'));
myChart.setOption({
  // ...
});
```

> 패키지 크기를 최소로 유지하기 위해 ECharts는 트리 셰이킹 가능한 인터페이스에서 어떤 렌더러도 제공하지 않으므로, `CanvasRenderer` 또는 `SVGRenderer`를 렌더러로 선택하여 가져와야 합니다. 이것의 장점은 SVG 렌더링 모드만 사용해야 하는 경우, 필요하지 않은 `CanvasRenderer` 모듈이 번들에 포함되지 않는다는 것입니다.

샘플 에디터 페이지의 "전체 코드" 탭은 트리 셰이킹 가능한 코드를 생성하는 매우 편리한 방법을 제공합니다. 현재 옵션을 기반으로 동적으로 트리 셰이킹 가능한 코드를 생성하여 프로젝트에서 직접 사용할 수 있습니다.

## TypeScript에서 옵션 타입 생성하기

TypeScript를 사용하여 ECharts를 개발하는 개발자를 위해, 최소한의 `EChartsOption` 타입을 생성하는 타입 인터페이스가 제공됩니다. 이 타입은 정확히 어떤 컴포넌트가 사용되고 있는지 알기 때문에 기본 제공되는 것보다 더 엄격합니다. 이는 누락된 컴포넌트나 차트를 더 효과적으로 확인하는 데 도움이 됩니다.

```ts
import * as echarts from 'echarts/core';
import {
  BarChart,
  LineChart,
} from 'echarts/charts';
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  // Dataset
  DatasetComponent,
  // Built-in transform (filter, sort)
  TransformComponent
} from 'echarts/components';
import { LabelLayout, UniversalTransition } from 'echarts/features';
import { CanvasRenderer } from 'echarts/renderers';
import type {
  // 시리즈 옵션 타입은 SeriesOption 접미사로 정의됩니다
  BarSeriesOption, 
  LineSeriesOption,
} from 'echarts/charts';
import type {
  // 컴포넌트 옵션 타입은 ComponentOption 접미사로 정의됩니다
  TitleComponentOption, 
  TooltipComponentOption,
  GridComponentOption,
  DatasetComponentOption
} from 'echarts/components';
import type { 
  ComposeOption, 
} from 'echarts/core';

// ComposeOption을 통해 필요한 컴포넌트와 차트만 포함하는 Option 타입 생성
type ECOption = ComposeOption<
  | BarSeriesOption
  | LineSeriesOption
  | TitleComponentOption
  | TooltipComponentOption
  | GridComponentOption
  | DatasetComponentOption
>;

// 필요한 컴포넌트 등록
echarts.use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  DatasetComponent,
  TransformComponent,
  BarChart,
  LineChart,
  LabelLayout,
  UniversalTransition,
  CanvasRenderer
]);

const option: ECOption = {
  // ...
};
```