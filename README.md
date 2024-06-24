# SafeStep Landing Page

## 프로젝트 개요
SafeStep은 사회초년생들을 위한 근로 문제 해결 솔루션을 제공하는 플랫폼입니다. 이 프로젝트는 SafeStep의 랜딩페이지를 구축한 것으로, 사용자에게 서비스를 소개하고 문의사항을 접수받기 위한 목적으로 제작되었습니다. 특히, 사용자 행동을 기록하고 분석하여 더 나은 서비스를 제공하기 위한 로깅 시스템을 구현하였습니다.

## 주요 기능
1. **랜딩페이지 구성**
   - SafeStep 소개 및 서비스 설명
   - 고객 후기 및 팀원 소개
   - 자주 묻는 질문(FAQ) 섹션

2. **사용자 행동 로깅**
   - Google Apps Script와 Google Sheets를 이용하여 사용자 행동 로그 기록
   - 사용자가 페이지에 접속할 때마다 IP 주소, 방문 URL, 레퍼러, 타임스탬프, UTM 파라미터, 디바이스 정보를 기록

3. **문의사항 접수**
   - 사용자가 문의사항을 제출할 수 있는 폼 제공
   - 입력된 이메일과 메시지를 Google Sheets에 기록하여 데이터베이스 역할 수행

## 기술 스택
- **프론트엔드**: HTML, CSS, JavaScript, Bootstrap
- **백엔드**: Google Apps Script
- **데이터베이스**: Google Sheets

## 주요 파일 설명
- `index.html`: 랜딩페이지의 메인 파일로, SafeStep 서비스 소개와 사용자 행동 로깅 기능이 포함되어 있습니다.
- `css/style.css`: 페이지의 스타일을 정의한 파일입니다.
- `js/main.js`: 페이지의 주요 기능을 담당하는 JavaScript 코드가 포함되어 있습니다.

## 구현 내용

### 사용자 행동 로깅
사용자가 페이지에 접속할 때마다 다음과 같은 정보를 로깅합니다:
- IP 주소
- 방문한 URL
- 레퍼러(이전 페이지 URL)
- 접속 시간(타임스탬프)
- UTM 파라미터
- 디바이스 정보(모바일/데스크탑)

```javascript
const sendData = async () => {
  const ip = await getIPAddress();
  const data = {
    id: getUVfromCookie(),
    landingUrl: window.location.href,
    ip: ip,
    referer: document.referrer,
    time_stamp: getTimeStamp(),
    utm: utm,
    device: mobile
  };

  try {
    const response = await fetch('https://your-appscript-url/endpoint', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(data)
    });
    const result = await response.json();
    console.log(result);
  } catch (error) {
    console.error('Error:', error);
  }
};
