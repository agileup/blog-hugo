+++ 
draft = false
date = 2014-05-26T17:52:55+09:00
title = "[OpenCV] Detecting and Matching Interest Points"
slug = "" 
tags = ["opencv"]
categories = []
+++

> OpenCV 2 Computer Vision Application Programming Cookbook  
> Chapter 8. Detecting and Matching Interests Points  

---

## Summary

* Detecting Harris corners
* Detecting FAST features
* Detecting the scale-invariant SURF features
* Describing SURF features  

컴퓨터 비전에서, Interest points(keypoints, feature points)는 객체 인식, 영상 정합, 비주얼 트래킹, 3D 복원 등 수많은 문제를 해결하는데 사용된다.

`영상 전체를 분석 < 몇몇의 특정 포인트들을 선택해 그 점들에 대해서 분석`

이 챕터에서 몇가지 Interest point detector를 소개하고, 어떻게 image matching에 사용되는지 소개한다.



## Detecting Harris corners

해리스 코너 검출 알고리즘은 기본적으로 영상 내 객체 내에 작은 윈도우(창틀)를 씌우고 상하 좌우로 움직이면서 윈도우 내의 화소값의 변화를 분석하여 코너점을 찾는 방식으로 구현된다.

영상 내 객체의 밝기값이 변화가 없는 영역에서는 당연히 평탄한 영역이 되므로 윈도우를 상하좌우로 움직여도 화소값은 항상 일정할 것이다. 그럼 이러한 윈도우가 좌우로 이동하여 영상의 경계선을 만났다고 생각할 경우 당연히 좌우 방향으로 움직이는 윈도우 내 화소값에는 큰 변화가 생길 것이지만, 상하 방향으로 움직이는 윈도우에 대해서는 화소값의 변화가 없을 것이다. 그럼 이 윈도우가 좌우방향 뿐만 아니라, 상하 방향으로도 움직인다고 생각하면 상하 방향으로 움직이는 동안에 분명히 화소값의 변화가 큰 지점을 지나게 될 것이다. 즉, 이점이 최종적인 코너점이 되는 것이다.

![flat-edge-corner](http://cfile5.uf.tistory.com/image/2759A4385344AA94315FF9)

쉽게 생각해서 윈도우가 상하 좌우 어느 방향으로 움직여도 그 윈도우 내에 있는 화소값의 변화량이 크게 나타나는 점이 바로 코너점이 된다는 것이 해리스가 제안하는 코너점을 찾기 위한 아이디어이다. 해리스 코너 검출 알고리즘을 수식적으로 분석하고 나타내기 위해서는 여러 수학적인 지식이 요구되는데 특히나 테일러 급수(Taylor series)의 개념과 고유값(eigenvalue), 고유벡터(eigenvector), 국소적 자기 상관 함수(local autocorrelation function) 등의 개념을 알아야 한다.

Harris 코너 검출 방법의 특징을 살펴보면, Harris detector는 영상의 평행이동, 회전변화에는 불변(invariant)이고 affine 변화, 조명(illumination) 변화에도 어느 정도는 강인성을 가지고 있다. 하지만 영상의 크기(scale) 변화에는 영향을 받기 때문에 응용에 따라서는 여러 영상 스케일에서 특징점을 뽑을 필요가 있다.

```cpp
// Detect Harris Corners
cv::Mat cornerStrength;
cv::cornerHarris(image, cornerStrength,
                    3,     // neighborhood size
                    3,     // aperture size
                    0.01); // Harris parameter
// threshold the corner strengths
cv::Mat harrisCorners;
double threshold= 0.0001;
cv::threshold(cornerStrength,harrisCorners, threshold,255,cv::THRESH_BINARY);
```



## Detecting FAST features

FAST(Features from Accelerated Segment Test)는 영국 캠브리지 대학의 Edward Rosten이 개발한 방법으로 FAST라는 이름에서 알 수 있듯이 극도의 빠름을 추구한 특징점 추출 방법. 하지만 FAST가 정말 뛰어난 점은 FAST가 속도에 최적화되어 설계된 기술임에도 불구하고 그 특징점의 품질(repeatability: 다양한 영상 변화에서도 동일한 특징점이 반복되어 검출되는 정도) 또한 기존의 방법들(Harris, DoG, ...)을 상회한다는 점에 있다.

![fast](http://cfile24.uf.tistory.com/image/253AC33A534626FA0C7695)

FAST에서는 위 그림과 같이 어떤 점 p가 코너(corner)인지 여부를 p를 중심으로 하는 반지름 3인 원 상의 16개 픽셀값을 보고 판단. 그래서 p보다 일정값 이상 밝은(>p+t) 픽셀들이 n개 이상 연속되어 있거나 또는 일정값 이상 어두운(<p-t) 픽셀들이 n개 이상 연속되어 있으면 p를 코너점으로 판단.

FAST 알고리즘에서는 어떤 점 p가 코너점인지 여부를 판단하기 위해 같은 유형의 연속된 점들의 개수를 직접 세는 대신에 decision tree를 이용하여 코너점 여부를 빠르게 판단하는 방법을 사용한다. 이를 위해 픽셀의 밝기값을 p보다 훨씬 밝은 경우, p보다 훨씬 어두운 경우, p와 유사한 경우의 3가지 값으로 분류하고 이를 이용하여 원주 상의 픽셀들의 밝기분포를 16차원의 ternary 벡터로 표현하고 이를 decision tree에 입력하여 코너점 여부를 분류한다.

> 개발자 홈페이지: http://www.edwardrosten.com/work/fast.html  
> 동영상: http://blog.naver.com/neverabandon/100104313783



## Detecting the scale-invariant SURF features

#### SIFT(Scale Invariant Feature Transform)

1)  Scale Space Extrema Detection : 특징의 크가와 위치를 결정  
       - Gaussian Pyramid  
       - DOG(Different Of Gaussian)  
2) Key Point Localization  : 특징에 좋지 않는 점들을 제거  
3) Orientation Assignment : 방향성분을 결정  
4) Key Point Descriptor : 특징을 재표현 함  

장점은  영상크기(scale), 조명(illumination), 평행이동, 회전(rotation), 은폐(occlusion)에 강하다. 단점은  계산량이 많음

#### SURF(Speeded Up Robust Features)

SURF는 여러 개의 영상으로부터 스케일, 조명, 시점 등의 환경변화를 고려하여 환경변화에 불변하는 특징점을 찾는 알고리즘중 하나로서 일반적으로 성능이 우수하다고 알려진 SIFT와 견줄만한 성능을 보이면서 속도를 크게 향상시킨 알고리즘이다. SURF는 그레이공간상의 정보만 이용함에 따라 컬러공간상에 주어진 많은 유용한 특징들을 활용하지 못한다.

