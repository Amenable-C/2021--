# 2021 만도 자율주행 경진대회

## 1. 팀원 소개
<table>
  <tr>
    <td align="center"><p><b>김신우</b></p><small>🚗 기계공학</small><br/><small>horse6953@gmail.com</small></td>
    <td align="center"><p><b>조훈</b></p><small>🚗 기계공학</small><br/><small>horse6953@gmail.com</small></td>
    <td align="center"><a href="https://github.com/Amenable-C"><p><b>최연재</b></p></a><small>🛠 컴퓨터공학</small><small><br/>💻 Developer</small></td>
  </tr> 
</table>

<br><hr><br>

## 2. 개발 목표
<b>인공지능 기반 자율주행 자동차 개발</b>

<br><hr><br>

## 3. 기본 동작도
<div>
<img src="https://user-images.githubusercontent.com/61836238/183289185-03f5d433-ad73-4646-a6b6-00c480c211df.PNG" width="800" height="400" align='center'><br><br>
  <table>
    <tr>
      <td align="center"><img src="https://user-images.githubusercontent.com/61836238/183289217-a449808d-27e1-4eba-86d9-c8ed50dd9ade.PNG" width="400" height="400" align='center'></td>
      <td align="center"><img src="https://user-images.githubusercontent.com/61836238/183289220-6c1b69b1-782e-4fd3-993b-d67677f34d56.PNG" width="400" height="400" align='center'></td>
    </tr>
  </table>
</div>

<br><hr><br>

## 4. 개발내용
#### 1. 하드웨어 구성도
<img src="https://user-images.githubusercontent.com/61836238/183289287-3767c5b1-22f8-4add-9a18-ea38b66aea66.PNG" width="400" height="400" align='center'>

#### 2. CATIA 설계
<div>
  <table>
    <tr>
      <td align="center"><img src="https://user-images.githubusercontent.com/61836238/183289313-884b1480-5365-4af9-a638-e45be52f1b8c.PNG" width="400" height="400" align='center'></td>
      <td align="center"><img src="https://user-images.githubusercontent.com/61836238/183289314-a53f5427-cfe2-44a4-94fb-8f1019ad0d1c.PNG" width="400" height="400" align='center'></td>
    </tr>
  </table>
</div>

#### 3. 소프트웨어 구성도
<img src="https://user-images.githubusercontent.com/61836238/183289511-593f148a-85a4-48ef-a496-3de188debeae.PNG" width="400" height="400" align='center'>


#### 4. 기술 구현
<b>(1) 차선인식</b>
- 원본 영상 읽어오기
- 흰색, 노란색 범위에 있는 것만 필터링
- Grayscale
- Blur
- Canny Edge Detection으로 외각선 검출
- 하단부 ROI
- Hough Transform

<b>(2) 핸들 조작</b>
- 조향 장치를 고려하여 테스트를 시행함으로써 오차값 줄이기
- 차폭과 회전반경 반영하기

<b>(3) 정지선 인식</b>
- 화면 하단에 ROI 영역 설정
- 하얀색 픽셀이 지정된 값보다 많으면 정지선으로 인식

<b>(4) 신호등 인식</b>
- 실제 트랙상 신호등 위치 및 형태확인 (신호등 위치: 상단, 옆) (신호등 형태: 삼색등, 사색등)
- ROI 설정
- Open CV에 있는 기능를 이용하여 신호등을 인식
- 명도를 활용하여 신호등의 상태정보 확인

<b>(5) 언덕 구간</b>
- IMU 센서와 카메라를 활용하여 언덕 구간 인식
- 언덕길로 인하여 카메라가 라인을 잡지 못하는 경우, 이전 영상과 초음파 센서를 기반으로 주행

<b>(6) 장애물</b>
- 라이다를 활용한 장애물 감지
- 장애물이 튀어 나오는 경우<br>
 $\to$ 초음파 센서를 활용하여 장애물 감지<br>
 $\to$ 회전각이 나오지 않으면, 일정한 거리를 후진하여 회전.

<b>(7) 로터리 진입</b>
- 라이다를 활용한 장애물 존재 여부 확인
- “좌측에서 차량이 다가오는 경우” 와 “우측에서 차량이 멀어지는 경우”를 나누어서 상황 구현

<b>(8) 주차</b>
- Lidar를 이용하여 생성한 Map을 기반으로 주차
- 초음파 센서 활용

<b>(9) 터널</b>
- 터널에 진입하여 차선 감지가 안될 시 LED ON
- 또한, 양쪽 초음파 센서를 이용하여 좌우 벽과의 거리를 측정하면서 주행
- 터널에서 빠져나와서 좌우 벽과의 거리가 측정이 되지 않으면, LED OFF

<b>(10) 표지판 인식</b>
- HSV를 통한 색 인식 및 구분
- Hough Transform을 이용한 모양 판단

<b>(11) 추돌방지 자율주행</b>
- 라이다와 초음파 센서를 활용하여 앞 차와의 추돌 가능성을 확인
- 거리에 따른 브레이크 값 조절

<b>(12) 교통표지판 인식 및 해석</b>
- 우선, YOLOv3을 이용하여 ‘교통표지판’이라는 객체 인식
- CNN 알고리즘을 이용하여 이미지 예측 모델 구현
- 학습된 모델을 이용하여 교통표지판 인식</br>
  $\to$ 그 후, 인식된 표지판에 해당하는 동작 수행

<br><hr><br>

## 5. 개발 환경
<table>
  <tr>
    <td align="center">OS</td>
    <td align="center">Robot Control</td>
    <td align="center">Video Processing</td>
  </tr>
  <tr>
    <td align="center">Ubuntu 18.04</td>
    <td align="center">ROS Melodic</td>
    <td align="center">Open CV</td>
  </tr> 
</table>

<table>
  <tr>
    <td align="center">SSD</td>
    <td align="center">차량 크기</td>
    <td align="center">배터리</td>
  </tr> 
  <tr>
    <td align="center">240GB</td>
    <td align="center">Width = 190mm, Depth = 328mm, Height = 135mm</td>
    <td align="center">18650 Battery x (4개 + 2개), 9v Battery</td>
  </tr> 
</table>

<br><hr><br>

## 6. 설계 모습 & 실제 동작
<div>
<img src="https://user-images.githubusercontent.com/61836238/183290481-fc0d5869-7498-4c6d-bf6c-7efab6eff066.jpg" width="400" height="400" align='center'>
<img src="https://user-images.githubusercontent.com/61836238/183290483-8744ed9e-3a08-4007-b381-6cd321e41fee.jpg" width="400" height="400" align='center'><br><br>
<img src="https://user-images.githubusercontent.com/61836238/183290485-4b403bcd-b8b0-435e-a52c-4cdee4d6c45b.jpg" width="400" height="400" align='center'>
<img src="https://user-images.githubusercontent.com/61836238/183290487-c94f3db1-6987-4a46-8e00-431847c342d5.jpg" width="400" height="400" align='center'>
</div>

<p align="left">
<img src="https://user-images.githubusercontent.com/61836238/183291179-1d7441a8-4859-4298-8532-b9165246621d.gif" width="400" height="400">
</p>

<br><hr><br>

<b>코드에 '주최측으로부터 제공된 내용'들이 있어서 코드를 업로드 하지 못한 점 양해부탁드립니다.<b>


