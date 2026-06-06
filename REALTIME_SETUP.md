# 실시간 공유 저장소 설정

현재 페이지는 Firebase Realtime Database가 설정되면 모든 기기가 같은 데이터를 봅니다.
설정값이 비어 있으면 기존처럼 각 브라우저의 localStorage만 사용하므로 서로 데이터가 보이지 않습니다.

## 1. Firebase 프로젝트 만들기

1. Firebase 콘솔에서 프로젝트를 만듭니다.
2. Realtime Database를 만들고 위치를 선택합니다.
3. 웹 앱을 추가한 뒤 Firebase config 값을 복사합니다.

## 2. firebase-config.js 수정

`firebase-config.js`의 `YOUR_...` 값을 Firebase에서 복사한 값으로 바꿉니다.
특히 `databaseURL`이 실제 Realtime Database 주소여야 합니다.

```js
window.RANKING_FIREBASE_CONFIG = {
  apiKey: "...",
  authDomain: "...firebaseapp.com",
  databaseURL: "https://...-default-rtdb.firebaseio.com",
  projectId: "...",
  storageBucket: "...appspot.com",
  messagingSenderId: "...",
  appId: "..."
};
```

## 3. Database Rules

간단히 공유 테스트를 하려면 Realtime Database Rules를 아래처럼 둘 수 있습니다.
이 설정은 링크를 아는 사람이 데이터를 쓸 수 있으므로 공개 페이지에서는 주의하세요.

```json
{
  "rules": {
    "ranking-100": {
      ".read": true,
      ".write": true
    }
  }
}
```

## 4. 업로드 후 확인

1. 수정한 `firebase-config.js`까지 GitHub에 업로드합니다.
2. 휴대폰 A에서 `admin.html?group=steam-l2-1`에 들어가 점수를 입력합니다.
3. 휴대폰 B에서 `student.html?group=steam-l2-1`을 열어 같은 그룹 데이터가 보이는지 확인합니다.

그룹마다 저장 경로가 다릅니다. 예를 들어 `steam-l2-1`과 `steam-l2-2`는 서로 다른 데이터입니다.
