## OAUTH 2.0에 대하여

- Resource Server
  - 정보가 저장되어 있는 곳
  - 로그인이 안되어있으면 Owner에게 로그인하라고 띄워줌
  - 로그인이 되있다면 정보 사용 동의서를 보내준다.
  - 동의를 하면 Server가 Client에게 코드(정보에 대한 비밀번호)를 보내준다.
  - 정보를 받으면 자기가 가지고 있는 3가지의 데이터와 비교하고 Owner가 승인한 Client인지 검증
  - 완료가 되면 Access Token을 Client에게 넘겨줌
  - Client에게 받은 Access Token을 확인하고 자기가 발급한적이 있는 값이면 그 값을 Client에게 돌려주고
    Client는 그 값을 받고 데이터를 가공해서 Owner에게 보내준다.

- Client
  - 사용자 일수도 있고, 사용자가 사용하는 컴퓨터도 클라이언트가 될 수 있음
  - Resource Server한테 Client Id, Secret을 받아옴
  - Secret은 절대 노출되면 안됨
  - 클라이언트는 코드와 자기가 가지고 있던 Id와 Secret 정보를 담아서 다시 Server에 보냄
  - 클라이언트는 Access Token을 Server에 제출해 원하는 정보를 얻어온다.

- Resource Owner
  - Client에게 접속을 하면 정보요청확인서를 받게 된다.
  - 승인을 하게 되면 Resource Server에 자동으로 접속된다.