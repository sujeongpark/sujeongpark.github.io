---
layout: post
title: "MySQL 서비스 재시작 오류"
author: "sujeongpark"
---

<br>

# MySQL80 서비스가 로컬 컴퓨터에서 시작했다가 중지되었습니다.

<br>
spring boot 프로젝트를 진행하면서 게시글을 DB에 저장하던 중 한글이 깨지는 현상이 발생했다. 그래서 검색해본 결과 my.ini 파일을 수정하면 된다는 글들이 있었고  <code>C:\ProgramData\MySQL\MySQL Server 8.0\my.ini</code> 파일을 메모장으로 열고 character 인코딩과 관련된 설정을 몇 줄 추가하고 저장했다. 그리고 MySQL80 서비스를 재시작하려고 하니까...
<br><br>

<em>
" MySQL80 서비스가 로컬 컴퓨터에서 시작했다가 중지되었습니다. 일부 서비스는 다른 서비스 또는 프로그램에서 사용되지 않으면 자동으로 중지됩니다. "
</em>

<br>
저 오류창이 뜨며 MySQL 서비스가 자꾸 중지되었다. 처음에는 ㅎㅎ 다시하면 되겠지.. 하다가 몇 번 시도해봐도 계속 오류창이 떴다. 그래서 황급히 다시 구글에 열심히 검색해 본 결과..!
<br><br>

> [mysql 서비스 시작 안 됨](https://okky.kr/article/618921)

[![reply.jpg](https://i.postimg.cc/VspWFzv9/reply.jpg)](https://postimg.cc/4nvcfkzn)


 <div style="text-align:center;text-decoration:line-through">두둥.....! 큰일났다...!</div>

<br><br>파일의 인코딩이 달라져 그런 것 같았다. 그래서 검색해서 이것저것 해보다가 도저히 안될 것 같아 MySQL을 삭제하려던 찰나 stackoverflow에서 이런 글을 발견했다.<br><br>


> [the MySQL service on local computer started and then stopped
Ask](https://stackoverflow.com/questions/35670755/the-mysql-service-on-local-computer-started-and-then-stopped)



[![solution.jpg](https://i.postimg.cc/YSjCCB70/solution.jpg)](https://postimg.cc/rdXkfbK2)

<br><br>
게시글을 올린 사람은 나와 똑같은 문제가 발생했었고, 답변을 보던 중 지금 내 문제를 해결할 수 있는 단서를 얻을 수 있었다. 곧바로 HEX-Editor 중 하나인 Notepad++을 설치하고 my.ini 파일을 열어보니 정말 맨 앞에 <code>EF BB BF</code>가 있었다..! 이것을 지우고 파일을 저장 후 다시 서비스를 시작하니 다행히 잘 돌아갔다.
앞으로 메모장으로 설정파일 건드리는 것에 주의해야할 것 같다.<br><br>