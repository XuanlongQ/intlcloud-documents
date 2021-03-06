## 소개

CDN 가속은 COS 버킷 중의 콘텐츠에 대한 다운로드, 배포, 특히는 동일한 콘텐츠를 반복적으로 다운로드하는 시나리오에 적용됩니다.

## 설정 설명

사용자는 다음 도메인을 관리하여 버킷 중 객체의 신속한 다운로드와 배포를 구현할 수 있습니다.
- 기본 도메인 이름: 즉 COS 오리진 서버 도메인 이름입니다. 버킷 생성 시, 시스템에서 버킷 이름과 지역에 따라 자동으로 생성한 것으로서 기본 가속 도메인 이름과 구분됩니다.
- 기본 가속 도메인 이름: CDN 가속 노드의 도메인 이름에 따라 시스템이 자동으로 생성하며 사용자는 활성화 또는 종료를 선택할 수 있습니다.
- 사용자 지정 도메인 이름: 사용자는 버킷에서 ICP 라이센스를 가진 사용자 지정 도메인 이름을 Tencent Cloud 중국 대륙 CDN 가속 플팻폼에 바인딩할 수 있으며 사용자 지정 도메인 이름을 통해 버킷의 객체에 접근할 수 있습니다.

기본 가속 도메인 이름 또는 사용자 지정 도메인 이름이 CDN 가속을 활성화했을 경우, 오리진 서버가 공개 읽기 버킷일 경우 직접 CDN 가속 도메인 이름 또는 사용자 지정 도메인 이름을 통해 오리진 서버의 객체에 접근할 수 있습니다. 오리진 서버가 비공개 읽기 버킷일 경우, CDN 오리진 요청 인증과 CDN 인증 구성 이 두가지 옵션을 활성화하기를 권장합니다.

- 오리진 요청 인증(활성화 전제는 CDN 서비스 권한 부여가 이미 추가됨): 요청한 데이터가 엣지 서버에서 캐시를 적중하지 않았을 경우, CDN은 오리진 요청에서 데이터 콘텐츠를 획득해야 합니다. COS를 오리진 서버로 사용하고 오리진 요청 인증을 활성화한 후, CDN 엣지 서버는 특별한 서비스 ID(CDN 서비스 인증을 통해 이 ID를 획득해야 함)를 사용하여 COS 오리진 서버에 접근하여, 비공개 접근 버킷 중의 데이터 획득 및 캐시를 구현합니다.
- CDN 인증 구성: 엣지 서버 접근을 통해 캐시 데이터를 불러올 때, 엣지 서버는 인증 구성에 규칙에 따라 접근 URL의 ID 인증 필드를 인증하여 권한을 부여받지 않은 접근을 차단하며 이로써 핫 링크 보호를 구현하고 엣지 서버 캐시 데이터의 보안성과 신뢰성을 향상합니다.

CDN 인증 구성과 CDN 오리진 요청 인증의 사용 시나리오는 충돌하지 않지만 두가지 구성의 상태가 다르면 데이터 보호 효과도 달라집니다. 자세한 사항은 다음 표와 같습니다.


| 버킷 접근 권한      | CDN 오리진 요청 활성화 여부| CDN 인증 구성 활성화 여부 | CDN 가속 도메인 이름을 통한 오리진 서버 접근 여부  | COS 오리진 서버 도메인을 통한 오리진 서버 접근 여부  | 적용되는 시나리오         |
| ------------------- | ------------ | ------------ | --------------- | --------------- | ------------ |
| 공개 읽기              | 비활성화        | 비활성화         | 접근 가능          | 접근 가능          | 전체 서버 공개 읽기 |
| 공개 읽기              | 비활성화         | 활성화         | URL 인증 필요 | 접근 가능          | 추천하지 않음       |
| 공개 읽기              | 활성화         | 비활성화      | 접근 불가          | 접근 가능          | 추천하지 않음       |
| 공개 읽기              | 활성화         | 활성화         | URL 인증 필요 | 접근 가능          | 추천하지 않음       |
| 비공개 읽기+CDN 서비스 권한 부여 | 활성화         | 활성화         | URL 인증 필요 | COS 인증 필요 | 모든 링키지 보호   |
| 비공개 읽기+CDN 서비스 권한 부여 | 비활성화         | 활성화         | URL 인증을 사용해야 함        | COS 인증 필요 | 추천하지 않음       |
| 비공개 읽기+CDN 서비스 권한 부여 | 활성화         | 비활성화         | 접근 가능          | COS 인증 필요 |오리진 서버 보호     |
| 비공개 읽기+CDN 서비스 권한 부여 | 비활성화         | 비활성화         | 접근 불가        | COS 인증 필요 | 추천하지 않음       |
| 비공개 읽기              |     비활성화       |    활성화/비활성화     | 접근 불가        | COS 인증 필요 | CDN 사용 불가 |

>!
>- 첫 행을 예로, 오리진 서버 버킷의 접근 권한이 공개 읽기일 경우, CDN 오리진 요청 인증과 CDN 인증 구성을 모두 활성화하지 않으면 CDN 도메인 이름을 통해 CDN 엣지 서버와 오리진 서버 버킷에 직접 접근할 수 있고 COS 도메인 이름을 통해 오리진 서버 버킷에 직접 접근할 수 있습니다.
>- 사용자가 도메인 이름에 CDN 가속을 활성화한 후, 모든 사용자는 이 도메인 이름을 통해 직접 오리진 서버에 접근할 수 있습니다. 만약 데이터에 일정한 프라이버시가 있을 경우, 반드시 **인증 구성**을 활성화하여 오리진 서버 데이터를 보호하십시오.

## 기본 가속 도메인 이름 활성화
### 작업 절차
1. 버킷 세주 정보 인터페이스 상단의 [도메인 이름 관리]를 한번 클릭하고 [편집]을 한번 클릭하여 기본 가속 도메인의 현재 상태를 활성화로 설정합니다. 오리진 서버 유형은 보통 **기본 오리진 서버**로 기본 설정되어 있습니다. 만약 오리진 서버의 버킷에 정적 웹사이트를 켰고, 정적 웹사이트에 가속을 원할 경우, **정적 웹사이트 오리진 서버**를 다음 그림과 같이 선택하십시오.
![](https://main.qcloudimg.com/raw/c2a680b936c033d0ad00b058c7112bb1.png)
>!만약 사용자가 Tencent Cloud CDN 서비스를 한번도 사용해 본 적 없다면, [도메인 이름 관리]에 액세스할 수 없으며 먼저 CDN 콘솔에 액세스하여 CDN 서비스를 활성화해야 합니다.
2. 버킷이 공개 읽기인 경우, **오리진 요청 인증**을 활성화할 필요가 없으며 마지막에 [저장] 버튼만 클릭하면 CDN 가속을 활성화할 수 있습니다.
>!버킷이 비공개 읽기인 경우 오리진 요청 인증과 CDN 서비스 권한 부여를 동시에 활성화하면 CDN을 통해 오리진 서버 접근 시 서명을 가지지 않아도 될 수 있으므로 CDN 캐시 리소스를 공중망에 배포하여 데이터의 보안성에 영향을 미치기 때문에 CDN 인증 활성화를 권장합니다.
3. 오리진 요청 인증 활성화
 1. 버킷이 비공개 읽기인 경우, **오리진 요청 인증**(CDN 서비스 권한 부여를 이미 추가한 것을 전제로)을 활성화해야 합니다. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 왼쪽 메뉴의 [버킷 리스트]에 액세스하여 도메인 이름 구성이 필요한 버킷을 한번 클릭하여 버킷 구성 인터페이스에 액세스 합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
 2. 버킷의 상세 인터페이스 상단의 [도메인 이름 관리]를 한번 클릭하고 [편집]을 한번 클릭하여 [오리진 요청 인증]을 활성화하고(CDN 서비스 권한 부여가 이미 추가되었는지를 확인), [저장]을 한번 클릭하면 CDN 가속을 활성화할 수 있습니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/439f408aae267d3052758a1fdaa93743.png)
 3. [저장]을 한번 클릭하면 기본 가속 도메인 이름이 배포된 것을 볼 수 있습니다. 동시에, 하단에 **CDN 인증**의 상태 알림이 나타나며 [인증 구성]을 한번 클릭하면 CDN 인증을 구성하기 시작합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/8ed30acab9085f97f052e9eda83e6740.png)
 4. 리디렉션 인터페이스에서 "인증 구성" 버튼을 클릭하여 해당 페이지로 들어간 후, 인증 Key와 유효 시간을 입력합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/7b8f499321fbe7a61e304397a945215f.png)
 5. [인증 계산기]를 클릭합니다. 만약 이전 단계에서 이미 구성했다면, 인증 Key와 유효시간은 자동으로 입력되며 일반적으로 접근할 객체의 Path만 입력하면 됩니다. 다음 [생성]을 한번 클릭하면 인증 URL을 획득할 수 있습니다. 인증 URL을 사용하면 대상 객체에 직접 접근할 수 있습니다. 만약 전에 입력하지 않았다면 인증 계산기에 인증 Key, 유효시간 및 대상 경로를 입력해야 합니다. 다음 그림과 같습니다.
![인증 계산기](https://main.qcloudimg.com/raw/572b32410086d49cbfc00a650eb6f514.png)

## 사용자 지정 가속 도메인 이름 활성화

>!
>- 여기서는 COS 콘솔에서 사용자 지정 도메인 이름 추가 및 CDN 가속 활성화 방법만 소개합니다. CDN 콘솔에서 사용자 지정 도메인 이름을 추가하려면 [도메인 이름 액세스](https://cloud.tencent.com/document/product/228/5734) 문서를 참조하십시오.
>- COS 콘솔을 통해 추가하는 사용자 지정 도메인 이름의 상한은 10입니다.

### 작업 절차

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 좌측 메뉴 [버킷 리스트]에 액세스한 후, 구성할 도메인 이름 버킷을 한번 클릭하여 버킷 구성 인터페이스에 액세스합니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
2. 버킷 페이지 상단의 [도메인 이름 관리]에 액세스하고 두번째 란 "사용자 지정 가속 도메인 이름"에서 [도메인 이름 추가]를 한번 클릭한 후 바인딩할 사용자 지정 도메인(예 ` www.example.com`)을 입력합니다. 다음 오리진 요청 인증을 선택하고 우측의 [저장]을 한번 클릭하면 도메인 추가를 완료하게 됩니다. 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/0bfbd7e43e19f9bf8e0d42e2957fc1b8.png)
>! 버킷이 비공개 읽기인 경우, 오리진 요청 인증과 CDN 서비스 권한 부여를 동시에 활성화하면 CDN을 통해 오리진 서버 접근 시 서명을 가지지 않아도 될 수 있으므로 CDN 캐시 리소스를 공중망에 배포하여 데이터의 보안성에 영향을 미치기 때문에 CDN 인증을 활성화하고 단계 3을 진행할 것을 권장합니다.
3. 사용자 지정 도메인 이름을 저장한 후 CDN 인증란에는 CDN 인증 기능 스위치가 나타나며 사용자 지정 도메인 이름의 CDN 인증을 활성화할 수 있습니다.
4. [CDN 콘솔](https://console.cloud.tencent.com/cdn/access)에 로그인하고 좌측 메뉴의 [도메인 이름 관리]에 액세스한 후 구성할 도메인 이름의 [관리]를 한번 클릭하고, [안전 구성]을 선택합니다. 인증 Key와 유효 시간을 입력하고 설정 완료 후 [확인]을 한번 클릭합니다. 다음 그림과 같습니다.
![자세한 인증 구성](https://main.qcloudimg.com/raw/61310b0c5960b4846a946bbacbc9fd00.png)
5. [인증 계산기]를 클릭합니다. 만약 이전 단계에서 이미 구성했다면, 인증 Key와 유효시간은 자동으로 입력되며 일반적으로 접근할 객체의 Path만 입력하면 됩니다. 다음 [생성]을 한번 클릭하면 인증 URL을 획득할 수 있습니다. 인증 URL을 사용하면 대상 객체에 직접 접근할 수 있습니다. 만약 전에 입력하지 않았다면 인증 계산기에 인증 Key, 유효시간 및 대상 경로를 입력해야 합니다. 다음 그림과 같습니다.
![인증 계산기](https://main.qcloudimg.com/raw/ad4a7703e469269bbf299e19869d00d6.png)

## 주의 사항
도메인 이름이 CDN 가속을 활성화한 후, 모든 사용자는 이 도메인 이름을 통해 직접 오리진 서버에 접근할 수 있습니다. 만약 데이터에 일정한 프라이버시가 있을 경우, 반드시 **인증 구성**을 통해 오리진 서버 데이터를 보호하십시오.
