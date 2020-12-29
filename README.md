# VueTypescript

## 개요

본 프로그램은 Typescript 학습을 위하여 작성 합니다.

## 프로그램 설치

- vue cli [참조](https://cli.vuejs.org/guide/installation.html)
- vuetify [참조](https://vuetifyjs.com/en/getting-started/installation/)
- firebase [참조](https://firebase.google.com/docs/web/setup?authuser=0)

## 설정

### firebase 설정

- fierbase.config.ts [참조](https://firebase.google.com/docs/web/setup?authuser=0)
  Firebase Hosting 기본 정보를 갖는다.
  ```
    // 내려 받은 후 자신의 Firebase Hosting 정보를 입력 후 화일명을 firebase.config.ts로 변경한다.
    // Firebase 자바 스크립트 SDK v7.20.0 이상의 경우`measurementId`는 선택 필드입니다.
    export default {
      apiKey: "API_KEY",
      authDomain: "PROJECT_ID.firebaseapp.com",
      databaseURL: "https://PROJECT_ID.firebaseio.com",
      projectId: "PROJECT_ID",
      storageBucket: "PROJECT_ID.appspot.com",
      messagingSenderId: "SENDER_ID",
      appId: "APP_ID",
      measurementId: "G-MEASUREMENT_ID",
    };
  ```
- @/plugins/firebase.ts

  ```
    import Vue from 'vue';
    import firebase from 'firebase/app';
    import firebaseConfig from '../../firebase.config';

    // Firebae 리소스 로드
    import 'firebase/auth';
    import 'firebase/firestore';
    import 'firebase/database';

    // Firebase 초기화
    firebase.initializeApp(firebaseConfig);

    // Firebase 축약
    export const auth = firebase.auth();
    export const db = firebase.firestore();
    export const rdb = firebase.database();

    // 명시적으로 설정하는 대신 기본 브라우저 환경 설정을 적용합니다.
    auth.useDeviceLanguage();

    Vue.prototype.$firebase = firebase;

    export default firebase;
  ```

- @/shims-firebase.d.ts
  플러그인과 함께 사용하기 위한 타입 확장 [참조](https://kr.vuejs.org/v2/guide/typescript.html)

  > 플러그인은 Vue에 전역 혹은 인스턴스 property와 컴포넌트 옵션을 추가할 수 있습니다. 이러한 경우 TypeScript에서 플러그인을 컴파일하려면 유형 선언이 필요합니다. 다행스럽게도 TypeScript에는 이미 존재하는 타입을 보충하기 위한 module augmentation이라는 기능이 있습니다.

  - 예를 들어, instance property인 \$myProperty를 string 타입으로 선언하고자 하는 경우:

    ```
      // 1. 'vue'를 보충된 타입 선언 전에 import해야 합니다.
      import Vue from 'vue';
      // firebase
      import firebase from 'firebase/app';

      // 2. 보충하고자 하는 타입이 있는 파일을 지정하세요.
      //    Vue의 constructor type은 types/vue.d.ts에 있습니다.
      declare module 'vue/types/vue' {
        // 3. Vue에 보강할 내용을 선언하세요.
        interface Vue {
          $firebase: typeof firebase;
        }
      }
    ```

    > 위의 코드를 선언 파일 형태로 (my-property.d.ts 처럼) include하면, `$myProperty`를 Vue 인스턴스 내에서 사용할 수 있습니다.
