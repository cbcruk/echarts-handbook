# Apache ECharts 다운로드

Apache ECharts는 다양한 설치 옵션을 제공하므로, 프로젝트에 따라 다음 옵션 중 하나를 선택할 수 있습니다.

- npm에서 설치
- CDN 사용
- GitHub에서 다운로드
- 온라인 사용자 정의

이러한 설치 방법과 다운로드 후 디렉토리 구조에 대해 각각 살펴보겠습니다.

## 설치

### npm에서 설치

```sh
npm install echarts
```

사용법에 대한 자세한 내용은 [ECharts 가져오기](${lang}/basics/import)를 참조하세요.

### CDN 사용

ECharts는 다음 무료 CDN에서 사용할 수 있습니다:

- [jsDelivr](https://www.jsdelivr.com/package/npm/echarts)
- [unpkg](https://unpkg.com/browse/echarts/)
- [cdnjs](https://cdnjs.com/libraries/echarts)

### GitHub에서 다운로드

[apache/echarts 프로젝트](https://github.com/apache/echarts)의 [릴리스](https://github.com/apache/echarts/releases) 페이지에서 각 버전의 링크를 찾을 수 있습니다. 원하는 릴리스 버전 하단의 Assets에서 Source code를 클릭하세요. 다운로드 후 파일을 압축 해제하고 `dist` 폴더에서 `echarts.js` 파일을 찾아 전체 ECharts 기능을 포함시키세요.

### 온라인 사용자 정의

패키지 크기를 줄이기 위해 일부 모듈만 도입하려는 경우, [ECharts 온라인 사용자 정의](${mainSitePath}builder.html) 기능을 사용하여 ECharts의 사용자 정의 다운로드를 만들 수 있습니다.