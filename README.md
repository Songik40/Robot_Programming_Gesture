# Robot_Programming_Gesture — 손 제스처 5클래스 분류 모델 (TurtleBot3 조작용)

`robotPG`(TurtleBot3 음성·제스처·LiDAR·SLAM ROS 2 통합 · 팀 프로젝트)에서 **제스처 기반 조작**을 담당하며 만든 손 제스처 분류 모델이다.

| 파일 | 무엇 |
|---|---|
| `keras_model.h5` | 5클래스 이미지 분류 모델(Keras · Teachable Machine 형식) |
| `labels.txt` | 클래스 이름: `0 Stop · 1 Forward · 2 Backward · 3 Left · 4 Right` — TurtleBot3 의 정지/전진/후진/좌회전/우회전 명령에 대응 |

## 사용
```python
from tensorflow.keras.models import load_model
model = load_model('keras_model.h5', compile=False)
labels = [l.split(' ', 1)[1] for l in open('labels.txt').read().splitlines()]
# 입력: 224×224 RGB 를 [-1, 1] 로 정규화(Teachable Machine 관례) → model.predict → labels[argmax]
```
학습 데이터(손 제스처 이미지)와 학습 절차: [확인 필요 — 저자가 채운다]

## `robotPG` 와의 관계
`robotPG/gesture_teleop_mediapipe/gesture_teleop_mediapipe.py` 는 MediaPipe 제스처 인식기로 `cmd_vel` 을 내는 노드다. 이 keras 모델은 그 앞 단계에서 만든 분류 모델이며, 최종 통합에서 어느 쪽을 썼는지: [확인 필요]

## 역할
제스처 기반 조작 담당(본인). 음성·LiDAR·SLAM 등 다른 모듈은 팀원 담당.
