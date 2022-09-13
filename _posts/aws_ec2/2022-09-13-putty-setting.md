---
layout: post
title: "PEM 키를 이용한 AWS EC2 서버 접속 putty 설정"
categories: [AWS]
tags: [AWS, EC2, Ubuntu]
description: AWS EC2 putty 설정

comments: true

toc: true
toc_sticky: true
---

## PEM 파일이란?

<hr>

-   AWS에서 서버 SSH에 접속을 위한 인증 방법으로 키 페어 생성을 통해 EC2 접근을 위한 개인키를 보관한 PEM 컨테이너 파일이다.

<br>

## Puttygen을 이용한 PEM 파일 PPK 파일로 변환하기

<hr>

PEM 파일을 이용해 EC2 인스턴스에 접근하기 위해 개인키 파일 형식인 ppk로 추출해 변환을 해야 한다.

변환을 위해 먼저 putty에서 제공된 puttygen을 이용해 변환하는 과정을 알아보고자 한다.

<br>

#### 먼저 puttygen을 실행한다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189962834-97df0e8d-bd69-4e52-af2f-4235fd8b62b4.png"
  />

<br>

#### 다음과 같이 Load 버튼을 누르고

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189962958-6f82b2cf-9544-4c9a-bd25-aeacce4b716a.png"
  />

<br>

#### 초기에 .ppk 파일만 보여주는데 모든 파일로 변경 후 .pem 파일을 불러온다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189963019-238eb56c-336e-47c8-a014-a53d742fd6ce.png"
  />

<br>

#### 다음과 같이 성공 메시지를 본다면 정상적으로 .pem 키를 가져왔다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189963064-7eaf17ee-397a-44b9-bb39-aab4670a5c89.png"
  />

<img
    src="https://user-images.githubusercontent.com/84614785/189963072-00689500-ecb1-458d-a1c2-c0f6be28cd76.png"
  />

<br>

#### 마지막으로 Save priavate key를 눌러 ppk 파일을 저장한다.

#### 그럼 PEM 파일의 개인 키를 간단하게 추출해 변환했다.

<br>

## PPK 파일을 이용한 EC2 인스턴스 접속 putty 설정

<hr>

<img
    src="https://user-images.githubusercontent.com/84614785/189963199-7ffb9f2b-6ad5-4b79-a029-767fcb52cdcd.png"
  />

<br>

#### putty를 실행해 Host Name 또는 IP adress를 입력한다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189963200-646c4447-887d-4ddd-a721-ec6f7c4e5722.png"
  />

<br>

#### Connection-Data에 로그인 username을 설정해 줄 수 있다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189963202-3faf0f14-c049-40e5-8e67-96b279549a64.png"
  />

<br>

#### Connection-SSH-Auth에 puttygen을 이용해 저장한 ppk 파일을 가져와 접속한다.

<br>

<img
    src="https://user-images.githubusercontent.com/84614785/189963205-11f06adf-a75b-4b42-b37d-724940bccd52.png"
  />

<br>

#### 그럼 다음과 같이 정상적으로 접속된 모습을 확인할 수 있다.
