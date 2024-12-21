
### CI/CD 란

#### CI

CI는 Continuous Integration 지속적인 통합
지속적인 통합이란
애플리케이션의 새로운 코드 변경 사항이 정기적으로 빌드 및 테스트 되어 공유 레포지토리에 통합하는것을 의미

> [!info]- CI에서의 공유 레포지토리란
> 코드 버전 관리 시스템 (GitHub, GitLab등)을 의미
> 	- 이는 개발자들이 코드를 공유하고 협업하기 위해 사용하는 Git 저장소입니다.
> 	- 여기서 "통합"은 여러 개발자의 변경 사항을 **정기적으로 병합**하여 **코드 충돌을 최소화**하고, 변경된 코드가 빌드 및 테스트를 통과하는지 확인하는 과정입니다.

#### CD

CD는 Continuous Delivery 혹은 Continuous Deployment 두 용어의 축약어
지속적인 서비스 제공 혹은 지속적인 배포라는 의미

Continuous Delivery는 공유 레포지토리로 자동으로 Release 하는 것

Continuous Deployment는 Production 레벨까지 자동으로 deploy 하는 것을 의미

> [!info]- CD에서의 공유 레포지토리란 
> 빌드된 결과물(아티팩트)을 저장하거나 배포를 준비하는 저장소
> 	- CD의 주요 목표는 빌드된 애플리케이션을 **자동화된 배포 파이프라인**을 통해 전달하는 것 
> 	- 소스 코드 자체가 아닌 **빌드 산출물**(예: Docker 이미지, APK 파일, JAR 파일 등)이 저장


%% ### GitHub Action이란

GitHub Action 공식 문서에서는 
깃허브 액션을
`GitHub Actions는 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 CI/CD(연속 통합 및 지속적인 업데이트) 플랫폼입니다.`
이렇게 소개하고 있다.

깃허브 리포지토리에 발생하는 이벤트를 트리거로 하여 작업을 실행하도록 워크플로우를 작성할 수 있다.
`리포지토리에 대한 모든 끌어오기 요청을 빌드 및 테스트하거나 병합된 끌어오기 요청을 프로덕션에 배포하는 워크플로를 만들 수 있습니다.` %%

### GitHub Actions

#### 장점
- **GitHub와 완벽한 통합** : Github 저장소 이벤트(PR, Push 등)를 기반으로 파이프라인 트리거 가능.
- **커뮤니티 액션 지원** : 다양한 오픈소스 플러그인(Action)을 활용해 기능 확장 가능.
- **간단한 설정** : YML 파일로 파이프라인을 쉽게 작성 가능
- **가격** : GitHub Actions의 기본 제공 런타임은 무료 플랜으로 시작 가능(GitHub Public Repository).
#### 단점
- 복잡한 파이프라인에서는 관리가 어려울 수 있음.

### Jenkins

#### 장점
- **완전한 오픈소스** : 무료로 제공되며, 다양한 기능과 플러그인을 통해 무제한 확장 가능.
- **높은 유연성** : 수천 개의 플러그인 사용 가능. 예: Docker, Kubernetes 통합, GitOps 등.
- **온프레미스와 클라우드 모두 지원** : 자체 서버에서 실행하거나 클라우드 환경에 배포 가능.

#### 단점
- **복잡한 설정** : Jenkins 초기 설치 및 구성은 복잡하며 시간이 많이 걸림.
- **플러그인 의존성** : 플러그인 관리와 업데이트가 복잡하고, 충돌 가능성 있음.







### 참고 자료
https://artist-developer.tistory.com/24
CD - Continuous Delivery와 Continuous Depolyment이 2가지가 다르다는 내용 
https://engineering.linecorp.com/ko/blog/build-a-continuous-cicd-environment-based-on-data
CI에서 처음 PR 요청을 보낼 때 빌드 후 테스트 1번, (추가한 코드 분석) - 유닛 테스트
이 다음에 코드 리뷰 후 머지 후 테스트 1번 이렇게 중복해서 테스트 해야함(추가한 코드를 원래 코드와 합쳐서 분석) - 통합 테스트, E2E

