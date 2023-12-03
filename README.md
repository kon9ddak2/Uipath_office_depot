Documentation is included in the Documentation folder

<견적서 메일 발송>
 -  메일로 수신한 작업지시서 파일을 읽는다.
 - 오피스디포 사이트에서 작업지시서의 물품코드를 검색한다.
 - 검색하여 나온 물품의 수량을 작업지시서 대로 입력하여 장바
구니에 담는다.
 - 장바구니 페이지에서 견적서를 클릭하여 PDF 파일로 생성한다.
 - 생성한 PDF 파일을 첨부하여 메일 발송한다.

REFrameWork Template
Robotic Enterprise Framework

Keeps external settings in Config.xlsx file and Orchestrator assets

<작업내용>
 - 메일로 수신한 작업지시서 파일을 읽는다.
 - 오피스디포 사이트에서 작업지시서의 물품코드를 검색한다
 - 검색하여 나온 물품의 수량을 작업지시서 대로 입력하여 장바구니에 담는다.
 - 장바구니 페이지에서 견적서를 클릭하여 PDF 파일로 생성한다.
 - 생성한 PDF 파일을 첨부하여 메일 발송한다.

<사전작업>
작업시작 전, QueItem을 사용하지 않을 것이므로
TransactionItem을 DataRow로 변경
QueItem의 상태값 변경 부분 커맨드아웃처리

How It Works
INITIALIZE PROCESS
 - Invoke KillAllProcesses workflow> Kill Process (크롬, 엑셀)

 - Invoke CheckFilePath.xaml (메일첨부파일 저장폴더 초기화, 견적서PDF파일 저장폴더 초기화)
견적서요청메일리스트_데이터테이블 생성
 - Invoke GetData.xaml (Outlook메일 "받은 편지함"에서 제목에 "견적서 발급 요청"이 포함되어 있는 메일의
첨부파일을 Data/Input 폴더에 다운로드)
 - Invoke InitiAllApplications workflow> Open Browser (크롬)

GET TRANSACTION DATA Invoke GetTransactionData workflow> Try 영역 IF 조건값 
반복을 하기 위한 조건
Init에서 생성한 dt_TransactionData의 row수 만큼 반복하는데
이 때, TransactionItem은 dt_TransactionData의 현재 row의 값으로 진행

PROCESS TRANSACTION

Invoke Process workflow> 
첨부파일 데이터테이블 값을 이용, 오피스디포 장바구니 추가
견적서 PDF파일로 저장
저장된 PDF파일 메일로 전송

END PROCESS
Invoke CloseAllApplications workflow> CloseTab(크롬)
