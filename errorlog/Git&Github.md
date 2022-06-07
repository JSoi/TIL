# Git & Github Error

### 발생 환경) Git Add & Commit 시 발생한 오류

> warning: LF will be replaced by CRLF in OOO
> The file will have its original line endings in your working directory

#### 원인) CRLF 개행 문자 차이로 인한 문제다.

#### 해결방법
> git config --global core.autocrlf true
