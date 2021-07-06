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
