---
title: Vector 와 Quaternion의 연산
date: 2021-07-06 00:21:00 +0900
categories: [Tips,Tips-Unity]
tags: [tips]     # TAG names should always be lowercase
---

```
자주 사용하는 Vector 와 Quaternion 연산에 대한 정리입니다.

틀린 점이나 좋은 정보가 있다면 언제든지 댓글로 공유해 주세요!
```

# Vector
### Quaternion(A) * Vector(B)
* 결과 자료형 : Vector
* 결과 값 : B 벡터를 A 만큼 회전한 벡터 값

***
# Quaternion

### Quaternion(A) * Quaternion(B)
* 결과 자료형 : Quaternion
* 결과 값 : A 값과 B 값이 더해진 각도

### Quaternion 연산 주의 점
* **Quaternion.EluerAngle**를 사용해 Vector로 변환 후 **값을 조절하여** 다시 Quaternion으로 바꾸게 되면 결과 값이 **정확하지 않음.**
