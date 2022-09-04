## paperweight

`paperweight` 는 3개의 Gradle 플러그인으로 구성됩니다.
- `paperweight-core`: 페이퍼를 만드는 데 사용
- `paperweight-patcher`: 페이퍼 또는 기타 포크를 만드는 데 사용
- `paperweight-patcher`-기본 포크
- `paperweight-userdev`: Mojang 매핑을 사용하여 내부 플러그인을 개발하는 데 사용됨

### 테스트에 사용하는 방법:

- 메이븐 로컬에 `paperweight` 설치:
```bash
./gradlew publishToMavenLocal
```
- 테스트 프로젝트에서 플러그인 확인을 위해 'mavenLocal()'을 추가합니다.
(자세한 내용은 `Gradle docs`(https://docs.gradle.org/current/userguide/plugins.html#sec:custom_plugin_repositories) 참조)
- `paperweight` 조정 테스트 프로젝트의 버전
  - 의 로컬 버전
  `paperweight` 필요를 사용할 것이다. `-SNAPSHOT` 에서 온 버전의 접미사 `gradle.properties` 로 대체하다 `-LOCAL-SNAPSHOT`

> Most output `paperweight` creates goes into `<project-root>/.gradle/caches/paperweight`

### 디버깅

IntelliJ에서 포트 5005에 연결하는 원격 JVM 디버그 실행 구성을 생성한 다음 디버깅 모드에서 Gradle을 실행합니다.

```bash
./gradlew --no-daemon -Dorg.gradle.debug=true <task>
```

Gradle은 디버거가 연결될 때까지 시작되지 않으므로 중단점을 놓칠 염려가 없습니다.

### 스타일 가이드

이 프로젝트는 의견의 ['ktlint'](https://ktlint.github.io/) internter and formatter)를 따른다. 를 사용합니다.
['ktlint-gradle'](https://github.com/jlleitschuh/ktlint-gradle) 플러그인에서 코드를 자동으로 확인하고 포맷합니다.
이 레포

`format` 작업을 실행하여 대부분의 경우를 처리해야 하는 `ktlint`를 사용하여 프로젝트를 자동으로 다시 포맷합니다.
일관된 코드 스타일을 유지합니다. 커밋하기 전에 `ktlint`가 자체적으로 수정할 수 없는 오류를 수정하십시오.

```
./gradlew format
```

### IDE Setup

를 실행하는 것이 좋습니다. `ktlintApplyToIdea` 그리고 `addKtlintFormatGitPreCommitHook` IDE를 구성하는 태스크
`ktlint` 스타일 설정을 사용하여 커밋하기 전에 이 프로젝트의 코드를 자동으로 포맷합니다.

```
./gradlew ktlintApplyToIdea addKtlintFormatGitPreCommitHook
```

>이 프로젝트에서는 Gradle 7.0 이상을 위한 준비가 되었는지 확인하기 위해 많은 새로운 Gradle 기능을 사용하지만 찾을 수 없습니다.
> 우리는 업데이트하기가 너무 어려운 나쁜 위치에 처했습니다. 그렇긴 하지만, Gradle은 항상 새로운 API를 표시합니다.
> 다음 주요 버전까지 잠시 불안정하므로 "불안정 API 사용" 검사를 비활성화해야 합니다.
> 인텔리J에서도. 이 작업을 수행하는 가장 쉬운 방법은 "불안정 API"가 사용되는 모든 장소를 찾는 것입니다(tons in
> `Paperweight.kt`) 로 대체하고 거기서부터 검사를 비활성화합니다.
