# SystemProg_project02

- 소켓 네트워크 프로그램을 이용하여 클라이언트 - 서버 모델 기반의 채팅 프로그램을 제작
- 단체 채팅방과 같이 여러 클라이언트가 동시 접속을 통해 채팅을 하는 프로그램임



## server.c

[실행 방법]
```c
gcc -o server server.c -lpthread
./server 9999
```

-서버의 용도 : 전체 채팅을 관리해주는 역할
-서버에서 지원하는 명령어
> help, num_user, num_chat, notice, exit
> > help : 서버에서 지원하는 명령어를 보여줌  
> > num_user : 현재 채팅에 참가한 참가자 수를 보여줌  
> > num_chat : 현재까지 채팅에서 오간 대화수를 보여줌  
> > notice : 공지사항(서버에서 모든 클라이언트에게 메시지를 전송)  
> > exit : 서버 종료(진행 중인 채팅이 없을 경우에만 종료 가능)  

0. 명령어 처리
```c
void *thread_function(void *arg)
```
1.  소켓생성 및 listener   
```c
int  tcp_listen(int host, int port, int backlog) 
```
2. 새로운 채팅 참가자 처리
```c
void addClient(int s, struct sockaddr_in *newcliaddr)
```
3. 채팅 탈퇴 처리
```c
void removeClient(int s)
```
4. 최대 소켓 번호 찾기
```c
int getmax()
```

## client.c

[실행방법]
```c
gcc -o client client.c
./client 127.0.0.1 9999 bob
```   
-클라이언트 : 2개 이상 실행이 가능

1.소켓 생성 및 서버연결, 생성된 소켓 리턴
```c
int tcp_connect(int af, char *servip, unsigned short port)
```
2. 에러 송출
```c
void errquit(char *mesg)
```
