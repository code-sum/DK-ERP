# [⬅️](../README.md) DK-ERP 고객기업관리 구현

> 개발 담당자 : 이수경
>
> 개발 기간 : 2023-06-14
>
> 개발 우선순위 : 1순위
>
> ---
>
> < Contents >
>
> [1. 구현완료 화면](#1-구현완료-화면)
>
> [2. 소스코드](#2-소스코드)
>
> [3. 화면설계](#3-화면설계)
>
> ---



## 1. 구현완료 화면

![ERP_clnt_CREATE](https://github.com/code-sum/DK-ERP/assets/106902415/dc1dc797-633d-4ab9-ad19-7524f6ff1da8)

▲ 고객기업 목록 조회, 신규등록 기능 구현 (신규등록 시 주소 입력을 위해 Daum 우편번호 검색 활용)

![ERP_clnt_READ](https://github.com/code-sum/DK-ERP/assets/106902415/177bf784-97ac-44b8-b785-4459f89b4dd9)

▲ 고객기업 1건 조회 기능 구현 

- 1건 조회 시, 기업 주소별 지도와 마커를 화면에 표시 (Kakao Map API 활용)
- 1건 조회 시, 동일한 팝업 창에서 기업 정보 수정 및 삭제 가능





## 2. 소스코드

- Java
  - 파일경로 `/src/main/java/kr/happyjob/study/busClm`
  - [소스코드](../src/main/java/kr/happyjob/study/busClm)
- SQL
  - 파일경로 `/src/main/resources/sql/BusClm`
  - [소스코드](../src/main/resources/sql/BusClm)
- JSP
  - 파일경로 `/src/main/webapp/WEB-INF/view/busClm`
  - [소스코드](../src/main/webapp/WEB-INF/view/busClm)





## 3. 화면설계

![Figma_busClm](busClm.assets/Figma_busClm.png)

1️⃣ [신규등록] 버튼을 누르면, 신규 고객기업 정보를 입력할 수 있는 팝업 창이 열린다.

2️⃣ [우편번호 찾기] 버튼을 누르면, Daum 우편번호 서비스 창이 열린다.

3️⃣ 고객기업명, 사업자등록번호를 기준으로 전체 목록을 검색한다.

4️⃣ 고객기업명을 클릭하면, 상세정보를 확인할 수 있는 팝업 창이 열린다.

5️⃣ 기업 상세정보를 확인할 수 있는 모달 창에 카카오맵을 표시한다.





---

⬆️ [(위로가기)](https://github.com/code-sum/DK-ERP/blob/master/notes/busClm.md)