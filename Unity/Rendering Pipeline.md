## 1. What is rendering pipeline in unity?
* 콘텐츠를 가져오는 일련의 작업을 수행
* 씬의 내용들을 취하여 컬링(culling), 렌더링(rendering), 포스트프로세싱(post-processing)등 작업을 수행하고 그것을 표시
* 개발하기 앞서,**프로젝트에 적합한 렌더 파이프라인을 선택하는 것**이 중요
* [Unity 공식 문서 링크](https://docs.unity3d.com/Manual/render-pipelines-overview.html)
***


## 2. built-in render pipeline (빌트인 파이프라인)
* 유니티의 기본 파이프라인
* 사용자 지정 옵션이 제한된 범용 렌더 파이프 라인
* [Unity 공식 문서 링크](https://docs.unity3d.com/Manual/built-in-render-pipeline.html)
***


## 3. Universal Render Pipeline (유니버셜 렌더 파이프라인)
* Unity에서 사전 제작된 [Scritable Render Pipeline](https://docs.unity3d.com/Manual/ScriptableRenderPipeline.html)
* 아트스트 친화적인 워크 플로를 제공
* 모바일, 콘솔, PC 등 다양한 플랫폼에서 최적화된 그래픽을 빠르고 쉽게 만들 수 있음
* 싱글 패스 포워드 렌더링, [셰이더 그래프](https://unity.com/kr/shader-graph), VFX graph 지원
* [Unity 공식 문서 링크](https://learnandcreate.tistory.com/477)
* [Unity URP 설명서 링크](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@10.5/manual/whats-new/urp-whats-new.html)
***


## 4. High Definition Render Pipeline (고해상도 파이프 라인)
* 유니티에 내장된 SRP로 물리 기반의 렌더링과 우수한 GPU 성능으로 정확하고 매우 사실적인 그래픽을 제공
* AAA품질의 게임, 자동차 데모, 건축, 애플리케이션 및 고화질 그래픽이 필요한 모든 것에 사용하기 적합
* [Unity 공식 문서 링크](https://docs.unity3d.com/Manual/high-definition-render-pipeline.html)
* [Unity HDRP 설명서 링크](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@10.5/manual/index.html)
