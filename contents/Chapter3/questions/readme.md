# 3장 질문

p102.

> 분석용 데이터베이스 개발자는 아래 3가지 케이스를 고려하여야한다.

- 메인 메모리에서 CPU 캐시로 가는 대역폭을 효율적으로 사용하는 방법

    [https://stackoverflow.com/questions/50190692/effective-main-memory-to-cpu-maximum-bandwidth-in-c-sharp](https://stackoverflow.com/questions/50190692/effective-main-memory-to-cpu-maximum-bandwidth-in-c-sharp)

- CPU 명령 처리 파이프라인에서 분기 예측 실패(branch misprediction)과 버블 (bubble)을 피하는 방법
    - pipeline 예측(제어헤저드)

        대충 예측해서 미리 실행을 해두는거.
        예측을 성공하면 빠른데 실패하면 느려진다

        Last time predictor: 마지막 하나의 bit결과를 보고 판단하겠다

        Two-Bit Counter Based Prediction: 마지막 2개 bit들의 결과를 보고 판단하겠다

    - pipeline misprediction 피하는법

        [https://jissi.tistory.com/20](https://jissi.tistory.com/20)

        - 데이터를 sum할 경우 정렬된 데이터의 경우 예측률이 높아서 성능이 더 좋다.

        [https://course.ece.cmu.edu/~ece447/s13/lib/exe/fetch.php?media=onur-447-spring13-lecture11-branch-prediction-afterlecture.pdf](https://course.ece.cmu.edu/~ece447/s13/lib/exe/fetch.php?media=onur-447-spring13-lecture11-branch-prediction-afterlecture.pdf)

        - 분기문에서 더 자주 탈 condition을 위로 올려준다 = hint로 제공함 (p.36)

    - bubble

        [https://ezbeat.tistory.com/454](https://ezbeat.tistory.com/454)

        Bubble: 딥 파이프라인 안에 No-Operation 혹은 딥 파이프라이닝으로 초래된 이미 변경되었으나 파이프 안에 들어온 데이터, 즉 쓸모 없이 CPU만 점유하고 있는 데이터를 칭한다. 관념적으로는 이런 버블을 빨리 파이프라인에서 빼 주어야 효율이 상승한다.

    - bubble을 줄이는 방법
        - raw level에 내려가면 아래 방법이 무조건 좋다고 볼순없다..?

        ```jsx
        function timelog(fn, n) {
          console.time(fn.name);
          fn(n);
          console.timeEnd(fn.name);
        }

        const arr = Array(1000000).fill(1);

        function useFor(arr) {
          let sum = 0;
          for (let i = 0; i < arr.length; i += 1) {
            sum += arr[i];
          }
          console.log(sum);
        }

        function useForUnroll(arr) {
          let sum = 0;
          for (let i = 0; i < arr.length; i += 10) {
            sum += arr[i];
            sum += arr[i + 1];
            sum += arr[i + 2];
            sum += arr[i + 3];
            sum += arr[i + 4];
            sum += arr[i + 5];
            sum += arr[i + 6];
            sum += arr[i + 7];
            sum += arr[i + 8];
            sum += arr[i + 9];
          }
          console.log(sum);
        }

        timelog(useFor, arr);
        timelog(useForUnroll, arr);
        ```

        1000000
        useFor: 39.177ms
        1000000
        useForUnroll: 3.892ms

- 최신 CPU에서 단일 명령 다중 데이터(single-instruction-multi-data, SIMD) 명령을 사용하게 만드는 방법
    - [https://m.blog.naver.com/fs0608/221650925743](https://m.blog.naver.com/fs0608/221650925743)

    ![SIMD](./assets/Untitled.png)

    ![SIMD2](./assets/Untitled%201.png)

## 우리는.. 뭘해야할까?

→ db마다 parallel query라는걸 지원해.

- mysql 에서 thread 갯수를 설정할 수 있어
    - [https://www.percona.com/blog/2019/01/23/mysql-8-0-14-a-road-to-parallel-query-execution-is-wide-open/](https://www.percona.com/blog/2019/01/23/mysql-8-0-14-a-road-to-parallel-query-execution-is-wide-open/)
    - 쿼리별로는 안되는것같음

    ```jsx
    mysql> set local innodb_parallel_read_threads=1;
    mysql> set local innodb_parallel_read_threads=DEFAULT; --4
    ```

- oracle은 쿼리별로 parallel을 설정할 수 있어.

    ```jsx
    select /*+ FULL(emp) PARALLEL(emp, 35) */
             emp_name
          from
            emp;
    ```