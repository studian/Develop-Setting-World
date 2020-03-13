## Tensorflow

### 1. 일반적으로 사용하는 tensorflow

### 2. tensorflow를 `web`에서 사용하려면?
* TensorFlow.js 사용
* 예제 및 데모
- https://www.tensorflow.org/js/demos?hl=ko
- https://www.tensorflow.org/js/tutorials

### 3. tensorflow를 `모바일(Android/iOS/Raspberry Pi)`에서 사용하려면?
* TensorFlow Lite 사용
* 예제 및 데모
- https://www.tensorflow.org/lite

## Pytorch

### 1. random seed
* cpu에서 지정된 random number 확인 하는 코드
```
print("CPU Random Seed :", torch.initial_seed())
```
* GPU에서 지정된 random number 확인 하는 코드
```
print("CUDA Random Seed :", torch.cuda.initial_seed())
```

* 딥러닝은 weight initialization 할 때 random number가 많이 쓰인다
* 실험 결과를 재구현 하거나 개선이 되었는지 비교해보려면, 실험을 다시 할 때 동일한 random number를 사용해야 한다.
* 따라서, 다음의 코드로 random seed를 적용한다.

* cpu 사용시
```
torch.manual_seed(139083498)
```
* gpu 사용시
```
torch.cuda.manual_seed_all(3480249583742974)
```

