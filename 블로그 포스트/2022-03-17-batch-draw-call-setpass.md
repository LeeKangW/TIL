---
layout: post
title: Batch, Draw Call, SetPass
date: 2022-03-17 14:10 +0900
categories: [Unity, 최적화]
tags: [unity]     # TAG names should always be lowercase
---


# Draw Call

#### Draw Call 이란?
- CPU가 GPU에게 "**오브젝트를 그려라"** 라고 명령을 내리는 것
  - 그려라 명령 안에는 **하나의 오브젝트를 그리기 위한 정보**가 담겨져 있다.(Ex. 메시, 텍스쳐, 쉐이더, 라이트 등의 정보)
- 한 프레임이 그려지는 것은 CPU와 GPU의 작업이 끝난 경우
  - 게임 최적화를 위해서 CPU, GPU 중 어느 쪽에 부하가 생기는지 확인이 필요

- 이 값이 적을수록 가벼운 게임
- 기기의 성능에 따라 Draw Call 개수가 많아지면 프레임 드랍이 발생

#### Render States(렌더 상태)
- GPU가 가지고 있는 그려야 하는 상태의 정보 테이블
- Render States 테이블은 VRAM의 각각 데이터들의 메모리 주소를 저장

#### DP Call (Draw Primitive Call)
- CPU가 Render States 변경을 GPU에게 보내 저장하고 마지막으로 GPU에게 메시를 그리라는 명령을 보내는 것

#### Command Buffer
- CPU가 GPU에게 내린 명령이 잠시 대기하는 곳
  - CPU가 명령을 내렸는데 GPU가 작업 중에 있으면 GPU 작업이 끝나는 동안 CPU는 다른 작업을 할 수 없음.
  - 이런 현상을 방지하기 위해 
    - CPU는 Command Buffer로 명령을 저장하고
    - GPU는 Command Buffer에서 명령을 가져온다


# Batch

#### Batch 란?
- **DP Call**과 **상태 변경**들을 합친 넓은 의미의 Draw Call


# Batching

#### Batching 이란?
- 복수의 Draw Call을 하나의 Draw Call로 묶어서 처리하는 작업

#### Dynamic Batching

#### Static Batching



# SetPass

#### SetPass란?
- 렌더상태 변경의 발생 여부(메시 변경은 미포함)
- Material과 Shader와 관련된 것에 대한 Batch를 말한다

```
Batching이 일어나지 않을 때, Set pass Call과 Materials의 관계

Ex 1) Material을 공유하는 오브젝트가 10개
- Batch는 10개, Set Pass Call은 1개 -> 총 Batch는 11개

Ex 2) Material이나 Shader가 다른 오브젝트가 10개
- Batch는 10개, Set Pass Call은 10개 -> 총 Batch는 20개

```
=> 그러므로, **아틀라스**를 사용해 여러 오브젝트들을 **한 개의 Material로 묶어서 Set Pass Call을 줄이는 것**이 중요
