# 1. N초 동안을 어떻게 표현하는가?
- **Time.deltaTime / N** 을 사용   
```
float time = Time.deltaTime / N
```

# 2. 그럼 어떻게 사용?
- Coroutine을 사용
  -  N초 동안 이 작업이 진행되어야 함으로 코루틴을 써서 **비동기인 것처럼** 돌아가야 한다.

- float time = Time.deltaTime/N 에서 **time 이 1이 될 때까지** 반복문을 돌린다.

Ex)
```
public IEnumerator NTimeWork(float duration)
    {
        float time = 0.0f;

        while (time < 1.0f)
        {
            time += Time.deltaTime / duration;
            
            // ======= 하고자 하는 작업을 구현 =======
            
            
            
            yield return CoroutineStarter.WaitFor0ms;
        }
    }

```
