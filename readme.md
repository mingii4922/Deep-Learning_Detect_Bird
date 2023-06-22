# Introduction
---------------------------
본 프로젝트는 DeepLearning 기초 수업에서 개별적으로 진행한 kaggle 대회를 통해 bird 이미지 종류를 분류하는 DNN model을 만들어 성능을 향상시키는 것이 목적이다.
이 프로젝트를 통해 수업에서 배웠던 DeepLearning 알고리즘의 다양한 방법 및 알고리즘을 활용하여 문제를 해결하며 DeepLearning에 대하여 좀 더 깊은 이해을 얻고자 한다.

이 프로젝트는 기존의 kaggle 대회와 동일하게 public leaderboard와 private leaderboard가 있는데 최종 결과는 private leaderboard으로 순위를 매긴다.

또 이 프로젝트의 제약사항으로 기존의 opensource로 제공되는 pretrained model을 사용할 수 없다.
수업에서 배우고 사용한 방법을 통해 직접 network를 구성해야 하며, 결과적으로 자신이 사용한 기법이 직접 이해하고 사용한 것인지가 가장 중요하다.

### code에 대한 자세한 내용은 ipynb파일에 주석 내용을 참고.

----------------------------
# Image
----------------------
![](https://images.velog.io/images/mingii4922/post/cf940f4a-b5eb-4694-b78e-d3a0aca180d8/image.png)
--
총 15가지의 새 종류를 DeepLearning 알고리즘을 사용하여 분류

------------------------------
# Regularization
classification 성능을 향상하기 위해 dataset에 적합한 mean과 std로 정규화를 수행한다.
train set과 test을 나누기 전에 시행하며, 각 channel별로 mean과 std를 구한다.

# Data augmentation
pytorch 라이브러리의 transforms을 활용하여 데이터의 일반화 성능을 높이는데 도움을 준다.

# Neural Network 생성
image size를 224x224x3으로 고정하였기 때문에, maxpooling을 적용해 model의 계산복잡도를 줄인다.
maxpooling을 적용할 때 feature map size 및 channel size를 계산하며 직접 구현하였다.

결과적으로 max-pooling을 너무 많이 적용했을 때 성능이 저하되는 것을 발견하고, fc-layer의 weight 수를 늘려 정보손실을 어느정도 방지했다.

# Loss function
loss function은 classification에서 흔히 사용되는 CrossEntropy를 사용하며, network를 통해 나온 logit 값을 확률 값으로 변환한 후, entropy를 구한다.
optimizer는 Adam을 사용하였으며, learning rate는 1e-2부터 1e-6까지 10배씩 키우며 최적점을 찾는 과정을 시행했다.

# K-fold
machine learning 특성상 보지못한 데이터에 성능이 떨어지는 것을 방지하기 위해 k-fold를 활용했다.
k를 5로 두며, 총 5개의 모델을 soft-ensemble했을 때 single 모델보다 test set에서 성능이 향상되는 것을 관찰했다.


# ConClusion
---------------------------------
### Public Leaderboard

![](https://images.velog.io/images/mingii4922/post/89702279-7a94-4f49-a7fc-cccf87cf28ab/image.png)
--
### Private Leaderboard

![](https://images.velog.io/images/mingii4922/post/5bb4be4f-aa7a-45a9-9da0-f1fc687f3722/image.png)
--
대회를 참가할 때, pretrain model을 사용하지 않고 데이터 전처리부터 수업시간에 배운 다양한 기법들을 통해 37명 중에서 상위권을 차지하였다.

-----------------------------------
대회 링크
https://www.kaggle.com/c/detect-the-bird/leaderboard

