---
hide:
    - navigation
---

# DoneDone Guidelines

던던팀은 우리 모두에게 최고의 경험을 제공하고자 몇몇 가이드라인을 제안합니다.

!!! tip ""
    위 문장 속의 **우리**에는 던던 프로덕트의 사용자, 던던팀의 기획자/디자이너/개발자 모두가 포함됩니다.
    
## Experience

### Common

- 기획자와 디자이너의 역할을 확실히 나눕니다.
- 던던팀 모두가 사용하는 서비스를 만듭니다.

### User

- 사용자의 font scale을 존중합니다.
    - 컴포넌트 사이즈 하드코딩을 지양합니다.
        - 다양한 font scale 대응을 위해 패딩을 활용하여 사이즈를 결정합니다.
    - 아이콘 사이즈도 font scale을 따라가야 합니다.
        - 만약 1.2배수 font scale이 사용됐다면 아이콘의 사이즈도 1.2배수로 증가해야 합니다. 
- 최소 터치 영역을 보장합니다.
    - 최선의 접근성을 위해 최소한의 터치 영역을 보장해야 합니다. 부족한 터치 영역은 패딩으로 확보할 수 있습니다.
    - 최소 터치 영역은 48dp로 지정합니다.
- `contentDescription` 제공을 지향합니다.
    - 최선의 접근성을 위해 최소한의 semantic을 제공해야 합니다.

### Developer

- 조기 최적화를 피합니다.
    - 수백만 명의 요청을 걱정하기 전에 100명의 사용자가 우리의 제품을 좋아하고 계속 사용하고 싶어 하는지를 먼저 확인해야 합니다. 사용자 피드백을 검증하는 작업이 우선입니다.
    - 대부분의 조기 최적화는 불필요하며 눈에 띄는 성능 문제가 관측됐을 때 진행해도 늦지 않습니다.
    - 적어도 제품 초기 단계에서는 최적화에 투자할 시간으로 기능 개발이나 유저 피드백 반영을 우선시해야 합니다. 제품 초기 단계에서는 우리가 작성한 코드가 삭제될 가능성이 높습니다.
    - Reference: [#1](https://stackify.com/premature-optimization-evil/), [#2](https://softwareengineering.stackexchange.com/questions/80084/is-premature-optimization-really-the-root-of-all-evil)
- 오버엔지니어링을 피합니다.
    - 불필요한 추가 개발은 코드베이스의 복잡도를 증가시키고 코드 유지보수에 추가 비용을 초래합니다. 
    - 만약 지루함에서 오는 오버엔지니어링(흥미로운 도전의 결과)이라면 던던 안드로이드 개발팀 모두에게 새로운 경험인 [린트 개발](https://github.com/TodayDoneDone/convention-cosmos)에 참여하여 해소할 수 있습니다.
    - 진행하려는 개발이 [DEEP](#deep)에서 논의 완료된 부분인지 확인해야 합니다.
    - Reference: [#1](https://en.wikipedia.org/wiki/Overengineering), [#2](https://www.mindtheproduct.com/overengineering-can-kill-your-product/)
- 코드베이스의 80% 이상을 파악하고 있어야 합니다. (세부 구현 방법까지는 불필요, 단순히 파악에만 의의를 둠)
    - 코드베이스 이해가 부족하면 기능을 버그로 인식하거나, 버그를 기능으로 인식할 수 있습니다.
    - 한 사람만 일방적으로 피드백하는 상황을 예방할 수 있습니다.
    - 코드 재사용으로 중복 코드를 예방할 수 있습니다.
    - 특정 상황에 사용하도록 설계된 코드를 적합하게 사용할 수 있습니다.

## Kotlin Convention

- trailing comma 필수 사용
    - git diff를 줄일 수 있습니다.
- named argument, new-line argument 취향대로 사용
    - (추후 구체화된 규칙이 나오기 전까지 유효)
- 들여쓰기 2칸 사용
    - 한 번에 더 많은 코드를 파악할 수 있습니다.
    - 불필요한 newline을 최소화할 수 있습니다.
- 함수 반환 표현 정책
``` kotlin
// 한 단계 수식으로 완성되는 함수를 제외하면 모두 명시적 `return` 사용
// `when`이 사용되는 경우 `when`의 모든 블록이 한 단계 수식으로 완성되는 경우에만 `return` 생략 허용

fun disallow() = a.b.c.d.e.f.g
fun allow(number: Int) = number * 2

fun disallow(value: Boolean) = when(value) {
  true -> a.b.c.d.e.f.g
  false -> isTrue.asInt() * 2
}
fun allow(value: Boolean) = when(value) {
  true -> isTrue.asInt() * 1
  false -> isTrue.asInt() * 2
}
```
- 함수 newline 정책
``` kotlin
// ❌, 시각이 크게 바뀜 → 눈 피로도 증가
private suspend fun getData() = Data( // 👀
  a = 1, // 👀
  b = 2,
)

// ⭕, 시각이 크게 바뀌지 않음 → 눈 피로도 감소
private suspend fun getData() =
  Data( // 👀
    a = 1, // 👀
    b = 2,
  )
```
- `when` 괄호 정책
```kotlin
// 한 줄 표현 가능할 때는 괄호 생략
// 두 줄 표현 이상은 괄호 필수 사용

fun areYouAwesome(value: Boolean) {
  when(value) {
    true -> you_are_awesome()
    false -> {
      why_not()
      you_are_awesome()
    }  
  }
}
```
- `if`문 스타일 정책
```kotlin
// 괄호 필수 사용
// 조건이 2개 이상 들어가는 경우 각각 개행

fun disallow() {
  if (true) you_are_awesome()
}
fun allow() {
  if (true) {
    you_are_awesome()
  }
}

fun disallow() {
  if(are_you_awesome() && true) {
    awesome_magic()
  }
}
fun allow() {
  if (
    are_you_awesome() &&
    true
  ) {
    awesome_magic()
  }
}
```
- top-level 함수 100% 파일과 클래스 100% 파일 별도 분리
    - top-level 함수와 클래스가 섞여있는 파일 ❌
- 파일 네이밍 정책
    - [top-level 함수 100%] 합성어는 파스칼 케이스, 한 단어는 소문자
    - [top-level 확장 함수 100%] extension receiver 대상으로 네이밍
    > `File.kt`, `Int.kt`, `String.kt`, ... 
- 상수는 모두 대문자 + 스네이크로 표기
- spotless
    - detekt
    - ktlint

## Android Convention

- min-sdk는 23으로 진행
- Android Studio는 최신 stable 버전 사용
- MVVM + 멀티 모듈
    - Reference: [NIA](https://github.com/android/nowinandroid)
- 의존성 관리: Version Catalog, [Renovate](https://www.mend.io/renovate/)
    - 신규 의존성을 추가할 때 이유가 명확해야 함
- ktx나 shortcut을 사용하여 개발했을 시 코드 리뷰에서 원래의 방법을 물어볼 수 있음
- 테스트는 UI, Unit 모두 진행
    - UI Test: JUnit4
    - Unit Test: [kotest](https://kotest.io/)
- 패키지명
    - 안드로이드: `me.donedone.android`
    - 와플 (waffle): `me.donedone.waffle.android`
- Gradle 관리 방식
    - 기조: composite build 지향
    - build-logic ⭕
    - buildSrc ❌
    - Kotlin Script ⭕
    - Groovy ❌

## Android Resource Convention

### strings.xml

- 주제_설명
    - 모든 피쳐를 개별 모듈로 관리한다는 전제 조건

> notification_access_permission<br/>
> storage_permission_granted

### drawable

- 용도_타입_설명_사이즈
    - [용도]
        1. `bg`: 배경사진
        2. `ic`: 아이콘
    - [타입]
        1. `rounded`: 원형
        2. `baseline`: 기본값
    - [사이즈]
        - 사이즈는 dp를 기준으로 하며 끝에 dp 표기는 생략
    
> bg_baseline_gradient_500

### colors.xml

- 색이름_강도 (강도는 생략 가능)

> red
>
> blue_200<br/>
> blue_400<br/>
> blue_600

### View ID

- 타입_설명
    - 타입은 약어 사용
    - Material, AppCompat 등 접두사는 무시

> tv_header<br/>
> tv_title<br/>
> 
> btn_register

## Waffle Convention

!!! info

    [와플 🧇](https://github.com/TodayDoneDone/waffle-android)은 던던팀의 UI Kit 입니다.


- 와플이 완성되기 전까지 로컬 모듈로 개발
    - 완성 이후에는 개별 저장소 분리 및 메이븐 배포해서 사용
- 와플이 완성되기 전까지 material 사용 가능
    - 완성 이후에는 material 사용 지양
- 문서화 수준: TBD

## Git Convention

- branch 전략
    - release
    - main
    - develop
    - deep/$deep_number
    - fix/$issue_number
- merge 전략
    - feature → develop: squash
    - develop → main: merge commit
    - main → release: merge commit
    - bump pr → any: rebase
- 한글 커밋 메시지 사용
    - 고유 명사는 영어로

## DEEP

던던 개발팀은 [Hype Driven Development](https://blog.daftcode.pl/hype-driven-development-3469fc2e9b22)를 피하기 위해 각자 개발할 범위를 미리 정리하고 적당한 범위인지 검토받는 과정을 진행합니다. 이 과정을 DoneDone Evolution and Enhancement Process, 줄여서 DEEP이라고 지칭합니다.

> Inspired by [Kotlin/KEEP](https://github.com/Kotlin/KEEP).

### Convention

DEEP은 3가지 유형으로 나뉩니다.

1. 프로덕트 (`product`)
2. 자동화 (`automation`)
3. 라이브러리 (`library`)

DEEP은 다음과 같은 양식으로 작성돼야 합니다.

```
## 제목

### 요약 (생략 가능)

### 필요한 이유 (프로덕트 유형은 생략 가능)

### 목표

### 추후 목표 (생략 가능)

### 계획

### 논의 사항 (생략 가능)
```

DEEP은 [안드로이드 저장소 이슈](https://github.com/TodayDoneDone/donedone-android/issues?q=is:issue+label:DEEP)에 등록되고 관리됩니다.

### Reference

#### 영문

- [Hype Driven Development](https://blog.daftcode.pl/hype-driven-development-3469fc2e9b22)
- [A practical guide to writing technical specs](https://stackoverflow.blog/2020/04/06/a-practical-guide-to-writing-technical-specs/)
- [How to Write Awesome Tech Specs](https://eng.lyft.com/awesome-tech-specs-86eea8e45bb9)

#### 한글

- [Hype Driven Development - 설레발 주도 개발](https://lazygyu.net/blog/hype_driven_development)
- [뱅크샐러드의 특별한 스펙, '테크 스펙'](https://blog.banksalad.com/tech/we-work-by-tech-spec/)
