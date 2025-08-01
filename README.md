[README_aruco_pose.md](https://github.com/user-attachments/files/21544308/README_aruco_pose.md)

# 📷 ArUco 마커 실시간 검출 및 3D 포즈 추정 (OpenCV)

이 프로젝트는 OpenCV와 웹캠을 이용해 ArUco 마커를 **실시간으로 인식**하고, **마커의 3D 위치와 회전(포즈)**를 추정해 화면에 표시합니다.

---

## ✅ 기능 요약

- 웹캠으로 **ArUco 마커** 인식
- 마커의 **3D 위치(x, y, z)** 추정
- 마커의 **회전각(yaw, pitch, roll)** 표시
- **좌표축(axis)** 시각화
- 마커 ID, 위치, 회전 정보, 코너 표시

---

## 🧩 필요한 패키지

```bash
pip install opencv-python
```

추가 기능 필요 시:

```bash
pip install opencv-contrib-python
```

---

## 🗂 필요 파일

- `photo.py`: 마커 인식 코드
- `camera_calibration.pkl`: 사전에 만들어 놓은 카메라 캘리브레이션 파일  
  (포함된 값: `camera_matrix`, `dist_coeffs`)

---

## ▶️ 실행 방법

```bash
py photo.py
```

---

## 🖼 동작 예시

웹캠에 마커를 비추면 화면에 다음 정보가 출력됩니다:

```
ID: 24
Pos: (0.12, -0.03, 0.48)m
Rot: (11.3, -2.7, 178.9)deg
```

- 마커 테두리: 초록색
- 코너점: 빨간 원
- 좌표축: XYZ 방향으로 표시

---

## 🎯 주요 코드 요약

### ✔️ 포즈 추정 함수 (OpenCV 4.7 이상 호환)

```python
def estimate_pose_single_marker(corners, marker_size, camera_matrix, dist_coeffs):
    # 마커의 3D 점과 이미지 좌표 → solvePnP로 포즈 추정
```

### ✔️ 실시간 마커 검출

```python
cap = cv2.VideoCapture(0)
corners, ids, _ = detector.detectMarkers(frame)
cv2.aruco.drawDetectedMarkers(frame, corners, ids)
```

### ✔️ 좌표축, 위치, 회전 정보 표시

```python
cv2.drawFrameAxes(...)
cv2.putText(...)  # ID, 위치, 회전 등 표시
```

---

## 📌 참고

- ArUco 마커 생성기: [https://chev.me/arucogen/](https://chev.me/arucogen/)
- 마커 크기 단위: **미터(m)** 단위로 설정 필요 (`marker_size = 0.05` 는 5cm)

---

## 🧪 캘리브레이션 파일이 없다면?

`camera_calibration.pkl` 파일을 직접 만드는 코드도 제공 가능합니다. 필요 시 요청하세요!

---

## 🔚 종료 방법

- `q` 키 누르면 종료

---
