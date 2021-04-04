# **불량 검출 프로젝트**
  
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/1.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/2.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/3.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/4.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/5.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/6.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/7.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/8.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/9.png?raw=true" width="400"/>
<img src="https://github.com/kimbakcho/censysImageErrorFind/blob/main/resultImage/10.png?raw=true" width="400"/>

---

#목적

`이미지상의 불량 포인트는 찾는것`


---


# 기본 딥러닝 네트워크 전략 
  1. retinanet  
       -> 속도는 느리지만 작은 Object 검출에 성능이 좋음.(Feature Pyramid 특성을 활용)
  2. retinanet 구현 소스

     fizyr keras-retinanet이 현재 keras 2.4 로 마이그레이션 되면서 버그가 많아짐.

     tensorflow 1.15와 호환되는 keras-retinanet 버전(v0.5.1) 다운로드를 
     구현 소스 
     
     https://github.com/chulminkw/keras-retinanet-tf115.git 에서 수행.  

     [https://github.com/kimbakcho/keras-retinanet-tf115](https://github.com/kimbakcho/keras-retinanet-tf115)

     과거 버전을 Fork 해둠.

---

# 필요 유틸리티 
1. 이미지 라벨링 툴 (해당 사이트에서 이미지 라벨링 툴을 사용한다.)
  - https://github.com/tzutalin/labelImg 

---

# 학습 및 테스트팅 이미지 파일 

1. 이미지 height= 900px, width =900px 로 리사이징 하고 라벨링 한 첨부 파일 
   [https://github.com/kimbakcho/censysImageErrorFind/raw/main/resizeALL.zip](https://github.com/kimbakcho/censysImageErrorFind/raw/main/resizeALL.zip)

---

# 주요 시행 착오 

1. 이미지 사이지
   BackBone 으로 ResNet50 을 사용 하기 때문에 이미지 사이즈는 768 - 1024 

  
   **width: 900px, height: 900px** 
   
   으로 셋팅 (가장 적당함)

   이미지 1024px를 넘어 갈시에 학습이 안됨. 

<table>
<thead>
<tr>
<th>Backbone</th>
<th>Image Size (px)</th>
<th>Small validation mAP</th>
<th>LB (Public)</th>
</tr>
</thead>
<tbody>
<tr>
<td>ResNet50</td>
<td>768 - 1024</td>
<td>0.4594</td>
<td>0.4223</td>
</tr>
<tr>
<td>ResNet101</td>
<td>768 - 1024</td>
<td>0.4986</td>
<td>0.4520</td>
</tr>
<tr>
<td>ResNet152</td>
<td>600 - 800</td>
<td>0.4991</td>
<td>0.4651</td>
</tr>
</tbody>
</table>

---

# 학습 결과 성능 
mAP : 0.81 !!
```
Epoch 00029: saving model to /content/keras-retinanet/snapshots/resnet50_csv_29.h5
Epoch 30/30

35/35 [==============================] - 36s 1s/step - loss: 1.0427 - regression_loss: 0.9269 - classification_loss: 0.1157 - val_loss: 1.4366 - val_regression_loss: 1.2512 - val_classification_loss: 0.2229

Running network: 100% (59 of 59) |#######| Elapsed Time: 0:00:06 Time:  0:00:06

Parsing annotations: 100% (59 of 59) |###| Elapsed Time: 0:00:00 Time:  0:00:00

85 instances of class error with average precision: 0.8135

mAP: 0.8135
```





