#[시험2] 008_MFDS_IssueDetails_REF

**[How It Works]**

1. **INITIALIZE PROCESS**
    - Config.xlsx 설정
    - 브라우저(Chrome, Excel) 강제종료
    - 폴더, 파일 관리(폴더 있으면 삭제 후 생성, 파일 있으면 삭제)
    - [의약품 안전나라] 사이트 접속 > [고시/공고/알림] 클릭 > [행정처분정보] 클릭
    - 검색 조건 세팅 - 품목구분 = 의약품등, 처분일자기간 = 전월 1일 ~ 당월 마지막날까지 > [검색] 클릭
    - 검색 결과 데이터스크래핑 - [순번], [업체명], [URL] => TransactionData
        - 품목구분 select item에 config에 설정한 항목 없을 경우 => TransactionData=nothing
        - 검색 결과 없을 경우 => TransactionData=nothing
        
2. **GET TRANSACTION DATA**
    - Get transaction item 비활성
    - 처리할 TransactionItem 체크
      
3. **PROCESS TRANSACTION**
    - NavigateTo 행정처분정보 페이지로 이동
    - 필요한 항목 가져오기 [업체명], [처분일자], [위반내역], [처분사항] => "데이터테이블A"
      
4. **END PROCESS**
    - 브라우저 닫기
    - TransactionData isNot Nothing 일 경우 아래 진행
        - "데이터테이블A" 에서 이슈사항 필터링해서 "데이터테이블B"에 저장
        - "데이터테이블B" 에서 처분일자 필터링해서 "데이터테이블C"에 저장
        - 엑셀 각 시트에 해당 내용 쓰기
        - 결과파일 첨부하여 메일발송
