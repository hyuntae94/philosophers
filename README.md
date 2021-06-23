## philosophers

##### Mandatory part

1. 이 과제는 Norm에 따라 C로 코딩된다. 어떠한 누수,충동, 정의되지않은 행동 또는 표준오류는 0을 의미한다.
2. 몇몇 철학자들이 원탁에 앉아 세 가지 중 하나를 하고 있다: 먹는 것, 생각, 또는 잠.
3. 먹는 동안 그들은 생각을 하거나 잠을 자지 않고, 자는 동안 그들은 먹지 않고 있다. 물론 생각하는 동안 그들은 먹지도 않고 잠도 자지 않는다.
4. 철학자들은 큰 스파게티 그릇을 가운데 두고 원형 테이블에 앉는다.
5. 테이블위에는 몇 개의 포크가 있다.
6. 스파게티는 포크 한 개로 서빙하고 먹기가 어렵기 때문에 한 손에 하나씩 포크를 들고 먹는다 (총 2개)
7. 철학자 중 그 누구도 굻어서는 안된다. 즉 모든 철학자들은 먹어야 한다.
8. 어느 누구와도 대화해서는 안된다.
9. 철학자들은 언제 또 다른 철학자가 죽게 될지 모른다.
10. 철학자는 식사를 마칠 때마다 포크를 내려놓고 잠을 자기 시작합니다.
11. 철학자는 잠을 다 자고 나면 생각하기 시작할 것이다.
12. 철학자가 사망 했을 때 시뮬레이션이 종료된다.
13. number_of_philosophers: 철학자의 수이며 포크의 수이기도 합니다.
14. time_to_die: millisecond로 표현(1000ms == 1sec).철학자가 마지막 식사를 먹기 시작한 후 또는 시뮬레이션이 시작된 후 'time_to_die'를 먹기 시작하지 않으면 그는 죽는다.
15. time_to_eat: milliseconds로 표현(1000ms == 1sec). 철학자가 식사하는데 걸리는 시간. 식사하는 동안 두 개의 포크를 가지고 있어야 한다.
16. time_to_sleep: milliseconds로 표현. 철학자가 잠자는 시간.
17. number_of_times_each_philosopher_must_eat: argument는 option. 모든 철학자들이 적어도
’number_of_times_each_philosopher_must_eat’를 먹는다면 시뮬레이션은 중단된다. 만약 특정되지 않았다면 오직 철학자가 사망했을 경우에만 시뮬레이션이 종료된다.
18. 각각의 철학자들은 1에서 ’number_of_philosophers’까지 하나의 숫자를 부여받는다.
19. 철학자 번호 1은 철학자 번호 'number_of_philoshopers' 옆에 있다.
20. 숫자 N을 가진 다른 철학자는 철학자 N - 1과 철학자 N + 1 사이에 앉는다.
21. 철학자의 상태변화는 다음과 같이 작성되어야 한다.(X가 철학자 번호와 timestamp_in_ms(밀리초)로 대체되었습니다.)
    - timestamp_in_ms X has taken a fork
    - timestamp_in_ms X is eating
    - timestamp_in_ms X is sleeping
    - timestamp_in_ms X is thinking
    - timestamp_in_ms X died
22. 표현된 상태가 다른 철학자의 상태와 뒤엉키거나 뒤엉켜서는 안 된다.
23. 철학자의 죽음과 그 철학자의 죽음이 표현되는 시간 사이에 10밀리초 이상 차이가 날 수 없다.
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
---
###### mutex?
- https://sonny777.tistory.com/2
- mutex는 여러명의 threads(철학자들)이 하나의 변수(포크)에 접근하는것을 막아주는 커널 객체 중 하나이다.)
---
25. 각각의 철학자들 사이에 포크가 존재한다. 즉, 철학자들이 여러명이라면 각각의 철학자들 왼쪽과 오른쪽에 포크가 존재할 것이다.
26. 철학자들의 포크중복을 피할려면 각각의 포크에 mutex를 사용하여 포크상태를 방어해야한다.
27. 각각의 철학자들은 하나의 thread이다.