# What is color space?

![캡처_2020_09_28_08_00_06_428](https://user-images.githubusercontent.com/71207918/94378003-baf46880-0160-11eb-9a9a-10b863c3f73e.png)

사람이 인식하는 색들을 비슷한 순서대로 붙여서 배열해보면 원을 이룹니다. 이렇게 원을 이룬 색의 배열을 색상활(Color circle)이라고 합니다. 하지만 채도와 명도는 반대로 직선 방향으로 증가 또는 감소하는 형태로 인식하고 표현할 수 있습니다. 색의 3요소를 이러한 특성에 근거해서 하나의 중심축을 기준으로 색을 원형으로 배치하고 수직 방향으로 명도에 따른 변화를, 중심축으로부터 수평 거리를 이용해 채도 변화에 따른 차이를 표현하면 원통 형태의 3차원 색 좌표를 만들 수 있습니다. 이렇게 색을 공간 좌표에 나타낸 것을 색공간 또는 색체계라고 합니다.

### 개머트(gamut)

모든 색공간에는 개머트라는 해당 시스템이 재연할 수 있는 색상의 범위가 있으며 '색영역'이라 표기하기도 합니다. 색공간 뿐만 아니라 디스플레이, 카메라, 동영상 포맷과 같은 곳에서 구현 가능한 색상의 범위를 나타내는 성능 지표의 기준으로도 적용되어 사용 및 구현 가능한 색 영역에 따라 'NTSE 72%, sRGB 100%, Adobe RGB 99% 지원'과 같은 방법으로 표기하기도 합니다. 당연히 개머트가 넓은수록 사용할 수 있는 색상의 수가 많으며 계조표현이 자연스럽기 때문에 우수한 색공간입니다.

### RGB

RGB 색체계는 빛의 특성을 이용해 색상을 표현하는 방법으로 적색(red), 녹색(green), 청색(blue)의 삼원색이 각각 최댓값이면 흰색으로 되는 가산혼합법으로 색을 조합합니다. 디지털 영상에서 가장 기본적인 색공간 포맷으로 RGB는 사용되는 삼원색들의 첫 글자를 의미합니다. 일반적으로 sRGB와 Adobe RGB가 주로 사용됩니다.

### sRGB(Standard RGB)

1996년 HP와 마이크로소프트에서 제안한 컴퓨터를 위한 RGB 색공간으로 HDTV 시스템에서 사용하는 Rec.709와 동일한 개머트를 갖는 색공간입니다. 하지만 감마 설정에서 약간의 차이가 있기 때문에 sRGB로 되어있는 데이터를 HDTV에서 사용하는 Rec.709로 그대로 가져오면 이미지가 약간 어두워지게 됩니다. 하지만 최근의 비디어 관련 장비와 편집 소프트웨어에서는 sRGB와 Rec.709 상호 변환이 필요한 경우 자동으로 감마 보정을 해주기 때문에 사용자가 이 부분에 신경을 써 줄 필요가 없어졌습니다. 하지만 이 자동 기능이 반대로 문제를 일으키는 경우도 있기 때문에 동영상 작업에서 색공간에 대한 기초적인 지식과 표준 모니터의 중요성이 강조됩니다.

### ICC 프로파일

ICC 프로파일(International Color Conortium profile)이란 색 재현 장치의 색 특성을 결정하는 모든 색의 색채 좌표값이 저장되어 있는 데이터로 재생을 포함한 색공간 변환에 사용하는 미세 조종값이 저장되어 있습니다.

### 크로마 샘플링

밝기값(Y)과 색상값(Cb,Cr)을 서로 분리해 샘플링하는 것을 크로마 샘플링(Chroma sampling)이라고 하며 그 중에서도 4:2:2, 4:2:0과 같이 밝기값보다 낮은 밀도로 색상값을 샘플링하는 것을 크로마 서브 샘플링(Chromasub sampling)이라고 합니다

### 인쇄매체 색공간 CMY, CMYK

CMY는 3개의 기준 색을 혼합해 나머지 다른 색을 만든다는 점에서 RGB 기반의 색체계와 유사한 개념이지만 사용하는 색이 각각 청록(Cyan), 자홍(Megenta), 노랑(Yellow)이라는 것과 색을 섞으면 보다 어두워지는 감산 혼합법이라는 점에서 차이가 있습니다. 영상 기기보다는 프린터처럼 잉크 또는 토너를 사용하는 인쇄 매체를 위한 색공간으로 주로 사용됩니다. 감산 혼합법으로 표현할 수 없는 흰색은 배경이 되는 매체의 색을 그대로 노출시켜 사용합니다.
CMY는 기본적으로 세가지 색을 사용하는 색체계입니다. 하지만 C, M, Y의 세가지 색으로는 완전한 검은색을 표현하는데 한계가 있기 때문에 실제로는 검정이 추가된 CMYK를 더 많이 사용합니다.

# What is LUT?

LUT(Look-Up Table)는 색상(hue), 채도(saturation), 조도(brightness)를 수학적으로 정확하게 조정하여 촬영된 원본 이미지의 RGB값을 새로운 RGB값으로 만들어주는 방법이다. 

### 1. 1D LUT

![캡처_2020_09_28_08_19_31_251](https://user-images.githubusercontent.com/71207918/94378295-5981c900-0163-11eb-9086-7186388d0137.png)


R, G, B의 채널은 각각 하나의 1차원의 배열을 지니고 있습니다. 다시 말해 1D LUT는 1차원이기 때문에 개념상 면이 아닌 선 혹은 곡선의 형태이며 R, G, B 채널당 각각 커브를 움직일 수 있습니다. 1D LUT의 특징은 Lift, Gamma, Gain, Contrast에 1:1로 매칭이 되고, Hue, Saturation의 보정 값은 1D LUT에 아무런 변화를 주지 못합니다. 이러한 결과로 인해 흔히들 1D LUT를 흔히 밝기 값만 보정한다고 해서 ‘휘도 곡선’이라고 표현하고 있습니다. 하지만 Lift, Gamma, Gain 들을 R, G, B 채널 당 따로 보정을 했을 경우에는 휘도 외에도 색상까지 보정되는 결과를 얻을 수 있으므로 단지 휘도 값만 조절한다고 한정 지을 순 없습니다. 하지만 대다수 1D LUT는 R, G, B채널의 값이 동일한 경우가 대다수 입니다.

### 2. 3D LUT

![캡처_2020_09_28_08_20_55_101](https://user-images.githubusercontent.com/71207918/94378315-8afa9480-0163-11eb-9778-05ddd7761ede.png)

![캡처_2020_09_28_08_21_47_289](https://user-images.githubusercontent.com/71207918/94378321-aa91bd00-0163-11eb-8e1b-447aca3dc0fb.png)

3D LUT는 색상 채널의 모든 값 범위에 대한 색상 변환을 나타내는 각각의 축을 사용하여 선으로만 표현이 가능한 1D LUT와 달리 3차원 좌표계(3D Cube)로 시각화할 시킬 수 있습니다. R, G, B 각 축을 따라 있는 점의 개수는 LUT의 사이즈에 따라 다르게 생성됩니다. 그 점을 중심으로 각각의 색상 채널에 대한 색상 변환을 할 수 있으며, 점 과 점 사이는 보간법을 이용해 근사치 값으로 보정이 되므로 LUT의 사이즈가 클수록 좀 더 정밀하게 색상을 컨트롤 할 수 있습니다. 현재 우리가 LUT라고 통칭해서 부르고 많이 사용하는 LUT가 바로 3D LUT라고 보시면 됩니다.

# Logspace

The biggest reason to use the Log color curve is how it retains the most dynamic range of information from the camera sensor (or film negative). It encodes what the camera sees logarithmically, meaning that the correlation between the exposure of the image (measured in stops) and the recorded image  is completely constant over a wider range. It utilizes more of the sensor’s information than a standard video curve because it’s saving as much data as possible rather than capturing specifically for the human eye or a video screen. This gives you much more color data to work with in post-production.

![캡처_2020_09_28_08_29_48_870](https://user-images.githubusercontent.com/71207918/94378469-df524400-0164-11eb-98e3-4cb7fe6c95f6.png)

If you’re familiar with  curves, you know that the bottom left of the curve represents your blacks and shadows, and as you move to the top right of the curve, you have your highlights and whites. As you can see, a Log curve pushes the darker part of the image upwards to retain shadows. The top of the curve shifts down to retain highlights. Therefore, you retain more data from each side of the color curve.
Linear color space has constant and unchanged luminance values true to their exact mathematical values in the scene. To the human eye, this will look very dark and muddy in certain areas and overexposed in others because our eyes (and monitors for that matter) see colors differently than their exact luminance values and can see more detail in bright and dark areas. Therefore, we have to apply a different color space in order to see the color information in a more aesthetically pleasing way, as well as standardize color values for displays and monitors.


https://uploads.actionvfx.com/file/spina/photo/333/large_Graph.jpg

In the image above, the linear function is in blue, the exponential function (how light behaves) is in red and the logarithmic function (how light is best stored) is in green.  

If we assume the x-axis is the value of a color and the y-axis is the stored value, you can see that the linear function doesn’t change the value. It’s a very inefficient way to store color, since each perceptual increase is a doubling of value. This leads to both high values and a lot of wasted space in the brighter areas of the image. 

A shadow going from 0.1 to 0.2 is a huge step, but to get the same increase out of a value of 0.6 you need to go all the way up to 1.2 even though the visual difference is the same. You need six times the amount of data to fill in the hole between 0.6 and 1.2 that you do to fill in between 0.1 and 0.2. Hence, the reason why this is inefficient.

In linear color, adding “0.3” to the brightness of your image will be less and less effective the brighter the image gets, but in log color it will be equally effective as many times as you want to add that value. Because of this, most color grading work is done in logarithmic color space: it gives the most even control across the image.

Linear color space, on the other hand, is the best for most other VFX operations because it allows you to manipulate the pixel values as they would exist in the real world.



https://cogmltn1957.tistory.com/25
http://keruluke.com/archived_web/kft/vol4/lookuptable/
https://www.actionvfx.com/blog/the-difference-between-linear-and-logarithmic-color-space-and-why-you-should-care
https://www.rocketstock.com/blog/tips-for-log-color-space-compositing/
