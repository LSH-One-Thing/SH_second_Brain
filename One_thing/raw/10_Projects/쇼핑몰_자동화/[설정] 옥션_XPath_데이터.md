6.**데이터 주입:** 엑셀의 이름/전화번호로 입력 필드 채움. 
추가 요청 -> 엑셀 데이터의 이름/전화번호/배송메세지 
실제 엑셀 제목 : |   |
|---|
|주문자||   |
|---|
|수령 주소||   |
|---|
|수취인전화번호|
|   |
|---|
|배송메모|

9.**주소 검색/선택:** 행안부 API로 정제된 주소로 검색하고, 첫 번째 결과 클릭.
-> 정제된 주소로 검색이라는것을 조금 더 명확히 정의하자면 엑셀에 현재 주소가 |   |
|---|
|서울특별시 강서구 마곡중앙6로 85 마곡사이언스파크뷰 303-1호 ( 마곡동 )| 이렇게 되어있음 
여기서 서울특별시 강서구 마곡중앙6로 85 까지만 기본 주소에 포함되고 뒤에 마곡사이언스파크뷰 303-1호 ( 마곡동 )이것은 상세 주소로 들어가야함. 주소는 항상 바뀌니까 형식만 이렇게 하라는거임. 
첫 번째 결과 클릭후 '이 위치로 배송지 설정' 이라는 버튼을 클릭하면 주소 찾기 팝업창은 자동으로 닫힘. 그렇다는것은 config.ini 에도 이 버튼을 넣는 xpath값을 추가해야함. 

[System]

API_KEY = devU01TX0FVVEgyMDI1MTEyNjExMzU1NjExNjQ5NTk=

  

[Auction_Main]

배송지변경버튼_XPath = //*[@id="xo_id_open_address_book"]

  

[Auction_Form_Popup]

; [수정] 버튼

수정버튼_XPath = (//button[contains(@class, 'button__delivery-change')])[1]

  

; --- 입력칸 ---

배송지명_XPath = //*[@id="address-title"] | //input[@title='배송지명']

받는분_XPath = //*[@id="address-name"] | //input[@title='받는 분']

휴대폰_XPath = //*[@id="address-tel"] | //input[@title='휴대폰']

상세주소_XPath = //*[@id="address-detail"] | //input[@title='상세주소']

배송메시지_XPath = //*[@id="delivery-request"] | //input[@title='배송요청사항']

  

; 주소찾기 버튼

주소찾기버튼_XPath = //button[contains(text(), '주소찾기')]

  

; 저장 버튼

저장버튼_XPath = //button[contains(text(), '저장')]

  

[Auction_Search_Popup]

; [팝업2] 주소 검색창 (형님이 찾아낸 HTML 적용!)

; 입력창 Class: input_search

검색어입력칸_XPath = //input[contains(@class, 'input_search')]

  

; 검색버튼 Class: ico_search

검색버튼_XPath = //button[contains(@class, 'ico_search')]

  

; 검색 결과

첫번째검색결과_XPath = //ul[contains(@class, 'lst_search')]/li[1]//a

이위치로설정버튼_XPath = //*[@id="container"]/div/div/div[1]/div[3]/div[2]/a

현재 나한테 있는 config.ini에는 없는것 같음. 


### B. 데이터 필드 매핑 (코드 고정) 
이 부분도 현재 너한테 입력되어있는 고정값은 
|코드 변수|엑셀 컬럼명 (고정)|비고|
|---|---|---|
|`EXCEL_COL_NAME`|`주문자`|이름|
|`EXCEL_COL_PHONE`|`수취인전화번호`|연락처|
|`EXCEL_COL_ADDR`|`수령 주소`|원본 주소 (API 정제 대상)|

이 뿐이지만, 추가해야할게 있음 '배송메모 '라는 이름으로 고정되어 있어야함 
이 4가지는 현재 사용자의 엑셀 데이터에서 고정 값임 변경될일 없음. 


---

