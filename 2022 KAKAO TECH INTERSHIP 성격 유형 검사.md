
[프로그래머스 문제](https://school.programmers.co.kr/learn/courses/30/lessons/118666?language=javascript)

## 문제 설명

> 각 질문에서 선택에 따라 점수를 누적한 뒤, 
> 
> 성격 유형 쌍의 점수를 비교하여 최종 MBTI를 결정합니다.

## 문제 해결 과정

1레벨 문제들은 보통 이해하기 쉬운데
이건 카카오 문제여서 그런지
문제를 파악하는 것 조차 생각보다 오래 걸렸다

카카오 MBTI를 확인할 수 있는 질문을 survey 배열로 제공한다
이 질문에 대한 응답을 choices 배열로 제공

이 survey 배열의 원소는 길이가 2인 문자열이다
첫 번째 문자가 부정 응답의 결과 두 번째 문자가 긍정 응답의 결과이다.

choices의 원소는 1~7의 값을 가지고 1~3의 응답은 부정적인 응답 4는 모르겠다로 아무 영향도 주지 않는다 4~7은 긍정적인 응답으로
1 과 5 이면 1점 2와 6은 2점 3과 7은 3점이다
이렇게 모든 설문이 끝나면

점수가 높은 항목으로 성격 유형을 리턴해주면 되는데

잠을 자다가 객체에 각 유형의 값을 전부 0으로 넣은 다음
반복문으로 survey에 대한 결과를 객체의 요소에 반영해 계산하면 되겠다 라는 생각이 떠올라서 바로 실행했다

```js
function solution(survey, choices) {
    let result = "";
    const mbtiResult = {
        T : 0,
        R : 0,
        F : 0,
        C : 0,
        M : 0,
        J : 0,
        A : 0,
        N : 0
    };
    for(let i = 0; i < choices.length; i++){
        if(choices[i] === 7){
            mbtiResult[survey[i][1]] += 3;  
        }
        if(choices[i] === 6){
            mbtiResult[survey[i][1]] += 2;  
        }
        if(choices[i] === 5){
            mbtiResult[survey[i][1]] += 1;  
        }
        
        if(choices[i] === 3){
            mbtiResult[survey[i][0]] += 1;  
        }
        
        if(choices[i] === 2){
            mbtiResult[survey[i][0]] += 2;  
        }
        
        if(choices[i] === 1){
            mbtiResult[survey[i][0]] += 1;
        }
    }
    
    result += mbtiResult.R >= mbtiResult.T ? "R" : "T"
    result += mbtiResult.C >= mbtiResult.F ? "C" : "F"
    result += mbtiResult.J >= mbtiResult.M ? "J" : "M"
    result += mbtiResult.A >= mbtiResult.N ? "A" : "N"
    
    return result;
}
```

첫 번째 제출안이였다

테스트 케이스는 2개 모두 통과 했지만

![[Pasted image 20241225192249.png]]

35 점밖에 받지 못했다

점수 매핑 부분이 잘못된거 같아서

그쪽 부분을 수정해서

다시 테스트 했다

```js
function solution(survey, choices) {
    let result = "";
    const mbtiResult = {
        T: 0, R: 0, F: 0, C: 0, M: 0, J: 0, A: 0, N: 0
    };

    
    const scoreMap = [0, 3, 2, 1, 0, 1, 2, 3];

    for (let i = 0; i < choices.length; i++) {
        const [disagree, agree] = survey[i]; 
        const score = scoreMap[choices[i]];

        if (choices[i] < 4) {
            mbtiResult[disagree] += score; 
        } else if (choices[i] > 4) {
            mbtiResult[agree] += score; 
        }
    }

    
    result += mbtiResult.R >= mbtiResult.T ? "R" : "T";
    result += mbtiResult.C >= mbtiResult.F ? "C" : "F";
    result += mbtiResult.J >= mbtiResult.M ? "J" : "M";
    result += mbtiResult.A >= mbtiResult.N ? "A" : "N";

    return result;
}
```

```js
const scoreMap = [0, 3, 2, 1, 0, 1, 2, 3];

    for (let i = 0; i < choices.length; i++) {
        const [disagree, agree] = survey[i]; 
        const score = scoreMap[choices[i]];

        if (choices[i] < 4) {
            mbtiResult[disagree] += score; 
        } else if (choices[i] > 4) {
            mbtiResult[agree] += score; 
        }
    }
```

이 부분에서 scoreMap 은 초이스의 원소값이 1~7에 해당하는 점수가 매핑되어있다
scoreMap의 0 번째 원소에 0이 있는 이유는 초이스의 값이 1~7에 해당하는 점수를 매핑하려면 scoreMap의 1 번째 원소부터 7 번째 원소가 있어야 하므로 순서를 맞춰주기 위해 0을 0 번째 원소로 추가했다.

`const [disagree, agree] = survey[i]` 를 통해서
survey의 원소 문자열 첫 번째 문자는 disagree로, 두 번째 문자는 agree 변수로 배열 분해 할당 된다.

이렇게 수정 후 테스트 하니

![[Pasted image 20241225193039.png]]

정확도 테스트 통과에 성공했다.

