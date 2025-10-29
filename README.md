# 🎵 sketch_12230617_timer_counter

**Timer/Counter를 이용한 버저 음악 재생 – ‘고향의 봄’**

---

## 📘 개요
이 프로젝트는 **Arduino MEGA 2560**의 **Timer1**을 CTC(Compare Match) 모드로 설정하여  
OC1A 핀(PB5, 11번 핀)을 통해 **버저(Buzzer)** 로 특정 주파수를 출력하고,  
이를 조합해 **‘고향의 봄’** 멜로디를 연주하는 프로그램이다.

**Timer/Counter의 하드웨어 토글 기능**을 활용하여 정밀한 주파수 제어가 가능하다.

---

## ⚙️ 결선도

| Arduino MEGA 2560 | Peripheral Board | 설명 |
|--------------------|------------------|------|
| PB5 (핀 번호 11)   | LED8 (버저 핀)   | 음성 출력 신호 (OC1A) |

---

## 🧠 동작 원리

1. **Timer1을 CTC 모드**로 설정한다.  
   - `WGM13:0 = 0100`, 즉 TOP = OCR1A
2. **OC1A 핀 토글 모드 설정**  
   - Compare Match 발생 시 OC1A 출력이 반전됨 → 정사각파 발생
3. **Prescaler = 8**  
   - 주파수 조정을 위한 분주비 설정
4. **음 재생 함수**  
   - `play_music(주파수, 지속시간)`  
   - 지정한 음의 길이만큼 신호를 발생시킴
5. **쉼표 함수**  
   - `rest_ms(지속시간)`  
   - 출력 비활성화 상태로 유지 (무음)

---

## 🎼 주요 상수

| 이름 | 설명 | 값 (ms 또는 OCR1A) |
|------|------|--------------------|
| WHOLE_MS | 온음표 | 2727 |
| HALF_MS | 2분음표 | 1364 |
| QUARTER_MS | 4분음표 | 682 |
| EIGHTH_MS | 8분음표 | 341 |
| SCALE_C ~ SCALE_HIGHE | 도 ~ 높은 미 | 3821 ~ 1520 |
| GAP_DIV | 음 사이 간격 비율 | 40 |

---

## 🪗 주요 함수

### `play_music(uint16_t ocr1a_value, uint16_t length_ms)`
- OCR1A 값을 설정해 해당 주파수의 정사각파를 생성한다.  
- length_ms 동안 소리를 내고, 이후 잠깐 무음을 주어 음 사이 간격을 만든다.

### `rest_ms(uint16_t length_ms)`
- OC1A 출력을 비활성화해 완전한 무음을 유지한다.

---

## 🎶 연주 곡
**‘고향의 봄’ (Spring in My Hometown)**  
각 음의 주파수와 길이를 조합하여 4줄 구성으로 재생된다.

---

## 🧩 코드 동작 구조


---

## 🔊 출력 예시
버저에서 도~레~미~ 순의 음이 들리며,  
곡 전체가 반복 재생된다.  

Timer1의 Compare Match가 정확히 동작하므로  
음정과 박자가 일정하게 유지된다.

---

## 🧰 개발 환경
- **보드**: Arduino MEGA 2560  
- **IDE**: Arduino IDE 2.x  
- **언어**: C / C++  
- **주요 기능**: Timer1 CTC 모드, 하드웨어 토글, delay() 기반 시간 제어

---

## 📄 라이선스
MIT License (자유롭게 수정 및 사용 가능)
