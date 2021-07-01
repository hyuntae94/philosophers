# philosophers
- https://ko.wikipedia.org/wiki/%EC%8B%9D%EC%82%AC%ED%95%98%EB%8A%94_%EC%B2%A0%ED%95%99%EC%9E%90%EB%93%A4_%EB%AC%B8%EC%A0%9C
- https://www.youtube.com/watch?v=YAP0Bv_aQl8
### Summary
- 프로세스 스레드 기초에 대해서 배운다.
- 스레드 만드는 방법에 대해서 배운다.
- mutex에 관한 것.

#### Mandatory part

1. 이 과제는 Norm에 따라 C로 코딩된다. 어떠한 누수,충동, 정의되지않은 행동 또는 Norm 오류는 0점 처리 
2. 몇몇 철학자들이 원탁에 앉아 세 가지 중 하나를 하고 있다: 먹는 것, 생각, 또는 잠.
3. 먹는 동안 그들은 생각을 하거나 잠을 자지 않고, 자는 동안 그들은 먹지 않고 있다. 물론 생각하는 동안 그들은 먹지도 않고 잠도 자지 않는다.
4. 철학자들은 큰 스파게티 그릇을 가운데 두고 원형 테이블에 앉는다.
5. 테이블위에는 몇 개의 포크가 있다.
6. 스파게티는 포크 한 개로 서빙하고 먹기가 어렵기 때문에 한 손에 하나씩 포크를 들고 먹는다 (총 2개)
7. 철학자 중 그 누구도 굻어서는 안된다. 즉 모든 철학자들은 먹어야 한다.
8. 어느 누구와도 대화해서는 안된다.
9. 철학자들은 언제 다른 철학자가 죽게 될지 모른다.
10. 식사를 마친 철학자는 포크를 내려놓고 잠을 자기 시작합니다.
11. 철학자는 잠을 다 자고 나면 생각하기 시작할 것이다.
12. 철학자가 사망 했을 때 시뮬레이션이 종료된다.
13. number_of_philosophers: 철학자의 수이며 포크의 수이기도 합니다.
14. time_to_die: millisecond로 표현(1000ms == 1sec).마지막 식사를 시작하고 n 밀리 초 안에 먹기 시작하지 않거나 시뮬레이션을 시작한 후 n 밀리 초 안에 먹기 시작하지 않으면 죽는다.
15. time_to_eat: milliseconds로 표현(1000ms == 1sec). 철학자가 식사하는데 걸리는 시간. 식사하는 동안 두 개의 포크를 가지고 있어야 한다.
16. time_to_sleep: milliseconds로 표현. 철학자가 잠자는 시간.
17. number_of_times_each_philosopher_must_eat: argument는 option. 만약 모든 철학자들이 최소한 이 횟수만큼 식사를 했다면, 시뮬레이션은 끝난다. 만약 이 인자가 설정되지 않았다면, 철학자가 죽었을 때만 시뮬레이션이 끝난다.
18. 각각의 철학자들은 1에서 ’number_of_philosophers’까지 하나의 숫자를 부여받는다.
19. 철학자 번호 1은 철학자 번호 'number_of_philoshopers' 옆에 있다.
20. 숫자 N을 가진 다른 철학자는 철학자 N - 1과 철학자 N + 1 사이에 앉는다.
21. 철학자의 상태가 변경될 때마다 다음과 같이 출력한다.(X는 철학자가 부여받은 숫자로, timestamp_in_ms는 밀리세컨 단위의 소요된 시간을 기록)
    - timestamp_in_ms X has taken a fork
    - timestamp_in_ms X is eating
    - timestamp_in_ms X is sleeping
    - timestamp_in_ms X is thinking
    - timestamp_in_ms X died
22. 표현된 상태가 다른 철학자의 상태와 뒤엉키거나 뒤엉켜서는 안 된다.
23. 한 철학자의 죽음과 그 죽음에 대한 출력 사이에 10 밀리세컨 이상의 시간차가 있으면 안된다
24. 다시 한번, 철학자들은 죽는 것을 피해야 한다!
---
```
Program name: philo

Turn in files: philo/

Makefile: Yes

Arguments: number_of_philosophers, time_to_die, time_to_eat, time_to_sleep,[number_of_times_each_philosopher_must_eat]

External functs: memset, printf, malloc, free, write, usleep, gettimeofday, pthread_create, pthread_detach, pthread_join, pthread_mutex_init, pthread_mutex_destroy, pthread_mutex_lock,pthread_mutex_unlock

Libft authorized: No

Description philosopher with threads and mutex
```
---
###### threds?
- https://donghoson.tistory.com/8
- ![스레드1](https://user-images.githubusercontent.com/60500129/123378923-54558b80-d5c8-11eb-9fd6-e2eb346fff21.png)
- ![스레드2](https://user-images.githubusercontent.com/60500129/123378941-5881a900-d5c8-11eb-953e-31c73f37b90f.png)
- context switching?? https://www.youtube.com/watch?v=1grtWKqTn50 6분~
---
###### mutex?
- https://sonny777.tistory.com/2
- mutex는 여러명의 threads(철학자들)이 하나의 변수(포크)에 접근하는것을 막아주는 커널 객체 중 하나이다.
- ![뮤텍스 작동방식](https://user-images.githubusercontent.com/60500129/123379122-a26a8f00-d5c8-11eb-8563-a55260caaed3.png)
---
25. 각각의 철학자들 사이에 포크가 존재한다. 즉, 철학자들이 여러명이라면 각각의 철학자들 왼쪽과 오른쪽에 포크가 존재할 것이다.
26. 철학자들의 포크중복을 피할려면 각각의 포크에 mutex를 사용하여 포크상태를 방어해야한다.
27. 각각의 철학자들은 하나의 thread이다.
- https://42kchoi.tistory.com/301
- https://42kchoi.tistory.com/302
---
###### process?
- ![프로세스1](https://user-images.githubusercontent.com/60500129/123379022-76e7a480-d5c8-11eb-9322-80c8fb1ea65e.png)
- ![프로세스2](https://user-images.githubusercontent.com/60500129/123379027-78b16800-d5c8-11eb-8d0a-1b960d3f663c.png)
- ![프로세스3](https://user-images.githubusercontent.com/60500129/123379033-7a7b2b80-d5c8-11eb-8ad1-f1e2f26444c6.png)- 
- ![프로세스4](https://user-images.githubusercontent.com/60500129/123379042-7c44ef00-d5c8-11eb-8e43-50259d202c73.png)
---
bonus
- 모든 포크는 테이블 중앙에 있습니다.
- 메모리에는 state가 없지만 사용 가능한 포크 수는 세마포어로 표시됩니다.
- 각 철학자는 프로세스여야하며 메인 프로세스는 철학자가 아니어야합니다.
---
### 뮤텍스와 세마포어의 차이는?
- 세마포어는 공유 자원(포크)에 세마포어의 변수(포크수)만큼의 프로세스(또는 쓰레드 == 철학자)가 접근할 수 있습니다. 반면에 뮤텍스는 오직 1개만의 프로세스(또는 쓰레드)만 접근할 수 있습니다.
- 현재 수행중인 프로세스가 아닌 다른 프로세스가 세마포어를 해제할 수 있습니다.?? 
- 하지만 뮤텍스는 락(lock)을 획득한 프로세스가 반드시 그 락을 해제해야 합니다.
- https://velog.io/@hidaehyunlee/Philosophers-%EC%98%88%EC%8B%9C%EC%98%88%EC%A0%9C%EB%A1%9C-%EB%B3%B4%EB%8A%94-%EB%AE%A4%ED%85%8D%EC%8A%A4%EC%99%80-%EC%84%B8%EB%A7%88%ED%8F%AC%EC%96%B4%EC%9D%98-%EC%B0%A8%EC%9D%B4
---
###### fork()?
https://hunj.dev/blog/using_fork/
