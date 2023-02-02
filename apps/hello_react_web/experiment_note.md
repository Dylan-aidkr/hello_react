# Experiment 1
참고 자료:
https://itnext.io/add-react-to-phoenix-92c590fbbc7f
https://bpaulino.com/entries/modern-webapps-with-elixir-phoenix-typescript-react
https://betterprogramming.pub/phoenix-1-6-with-typescript-react-bea7f3a792d5


# 돌아가는 구조?
1. tailwind는 따로 빌드되서 상관없는듯
2. `config/config.exs`에 설정된 `config :esbuild ~~`의 설정에 의해 `js/app.js`를 진입포인트로 해서, esbuild가 돌아감
3. 이때 esbuild가 js, ts, jsx, tsx 가리지 않고, 알아서 빌드해서 번들링 해줌.
4. `app.js`는 `react/main.js`를 참조함
5. `react/main.js`는 `Remount`라는 라이브러리를 통해 리액트 컴포넌트들을 웹 컴포넌트(?)인것 처럼 등록해줌
6. 이렇게 등록된 컴포넌트는 일반적인 html 태그처럼 사용하되, prop은 stringify 된 형태의 json 문자열을 받아서 돌아가는듯, elixir가 렌더하는 과정에서는 Jason 라이브러리로 map을 string으로 변환해서 넣어주는 식으로 html 작성.
7. 최종적으로 완성된 app.js가 `priv/static/assets/app.js`로 들어감