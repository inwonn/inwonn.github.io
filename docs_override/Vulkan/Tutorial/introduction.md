---
title: Introduction
parent: Tutorial
nav_order: 0
---

# Introduction
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Vulkan이란
Khronos 그룹의 새로운 API. Vulkan은 최신 그래픽 카드의 훨씬 더 나은 추상화를 제공합니다.
{: .no_toc .fs-3 .fw-300 }

## Graphics API 비교
Vulkan은 성능과 하드웨어 제어를 극대화하는 데 중점을 둔 API로, 고성능 애플리케이션에 적합합니다.
{: .fs-3 .fw-300 }

<div markdown="1">

|**특징**|**Vulkan**|**OpenGL**|**Direct3D**|
|:-------------|:------------------|:------|:--------|
|**추상화**|`Low-Level`|`High-Level`|`High-Level`|
|**멀티스레딩**|`강력한 멀티스레딩`|`제한적 멀티스레딩`|`제한적 멀티스레딩`|
|**크로스플랫폼**|`Windows,Linux,Android등 광범위한지원`|`Windows, Linux, macOS등지원`|`Windows와 Xbox전용`|
|**드라이버 의존성**|`낮음`|`높음`|`중간`|
|**GPU성능활용**|`최적화된GPU성능제공`|`자동화된최적화`|`높은성능제공`|
|**그래픽파이프라인**|`명시적`|`상태 변경 가능`|`상태 변경가능`|
|**드라이버오버헤드**|`매우낮음`|`높음`|`중간`|

</div>

아래와 같이 개발자가 기존에 드라이버가 자동으로 해주던 작업들을 개발자가 직접 제어합니다. 드라이버의 역할은 CPU, GPU 간의 통신, 리소스 검증, 호환성 관리와 같이 최소한의 역할만 수행합니다.
{: .fs-3 .fw-300 }
<div markdown="1">

|**특징**|**Vulkan**|**OpenGL/Direct3D**|
|:-------------|:------------------|:------|:--------|
|**메모리 관리**|`개발자가 직접 제어`|`드라이버가 자동 관리`|
|**동기화 관리**|`명시적 제어`|`암묵적 제어`|
|**GPU 리소스 제어**|`직접적인 제어 가능`|`드라이버가 대부분 처리`|
|**환경별 동작 차이**|`일관된 동작`|`드라이버와 하드웨어에 따라 동작 이 다름`|

</div>

## 요약
 - Vulkan은 Khronos 그룹의 low-level graphics api 이다.
 - 드라이버가 자동으로 해주던 대부분의 일들을 개발자가 명시하게 되고 아래와 같은 기술을 습득 할 수 있다.
   - `GPU 동작 원리 이해`
   - `그래픽 애플리케이션의 성능 최적화 기술`
   - `크로스플랫폼 개발 경험`
   - `셰이더 및 그래픽 파이프라인 설계 기술`
   - `복잡한 문제 해결 및 디버깅 능력`

## 참고
 - [https://docs.vulkan.org/tutorial/latest/00_Introduction.html](https://docs.vulkan.org/tutorial/latest/00_Introduction.html)