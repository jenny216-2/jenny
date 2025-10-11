## P3.1 스프링–질량–감쇠기

원식:

$$
m\ddot x(t) + b\dot x(t) + kx(t) = F(t)
$$

상태변수:

$$
x_1(t)=x(t),\qquad x_2(t)=\dot x(t)
$$

> 따라서

$$
\dot{x}_1(t) = x_2(t), \qquad \dot{x}_2(t) = \ddot{x}(t).
$$



1차 미분방정식:

$$
\begin{aligned}
\dot x_1(t) &= x_2(t)\\
\dot x_2(t)=\ddot x(t) &= -\frac{k}{m}x_1(t) - \frac{b}{m}x_2(t) + \frac{1}{m}F(t)
\end{aligned}
$$

상태미분방정식:

$$
\dot x(t)=
\begin{bmatrix}
0 & 1\\
-\frac{k}{m} & -\frac{b}{m}
\end{bmatrix} x(t)
+
\begin{bmatrix}
0\\
\frac{1}{m}
\end{bmatrix} F(t),
\qquad
y(t)=\begin{bmatrix}1 & 0\end{bmatrix} x(t),\quad D=0
$$


## P3.3 직렬 RLC 회로 (전압원 입력)


### 1) 미분방정식 (KVL/KCL)

루프 KVL:

$$
v_1(t)=L\frac{di_L(t)}{dt}-v_c(t)+v_2(t)
$$

노드 KCL

$$
i_L(t)+C\frac{dv_c(t)}{dt}=i_R,   C\frac{dv_c}{dt}=-i_c(t)
$$

i_R을 구하기 위해 오른쪽 작은 loop에 KVL을 적용하면

$$
i_R=\frac{v_2(t)-v_c(t)}{R}
$$

위 식을 노드 KCL 식에 대입

$$
i_L(t)+C\frac{dv_c(t)}{dt}=\frac{v_2(t)-v_c(t)}{R}
$$

### 2) 상태미분방정식

$$
x(t)=
\begin{bmatrix}
i_L(t)\\
v_c(t)
\end{bmatrix}
\qquad
v(t)=
\begin{bmatrix}
v_1(t)\\
v_2(t)
\end{bmatrix}
\qquad
$$

$$
\dot x(t)=
\begin{bmatrix}
0 & \frac{1}{L}\\
-\frac{1}{C} & -\frac{1}{RC}
\end{bmatrix} x(t)
+
\begin{bmatrix}
\frac{1}{L} & -\frac{1}{L}\\
0 & \frac{1}{RC}
\end{bmatrix} v(t)
$$

## P3.5 피드백 제어 시스템

그림 P3.5에 피드백 제어 시스템이 주어져 있다.  
(a) 폐루프 전달함수 \( T(s) = \frac{Y(s)}{R(s)} \)를 구하라.  
(b) 상태변수 모델을 구하고, 위상변수 형태의 블록선도를 작성하라.

---

### (a) 폐루프 전달함수

피드백 제어 시스템의 일반식:

$$
T(s) = \frac{Y(s)}{R(s)} = \frac{G(s)}{1 + G(s)H(s)}
$$

회로에 주어진 데이터:

$$
G(s) = \frac{5(s+1)}{s(s+2)(s+8)},  
H(s)=1
$$

따라서 정리하면

$$
T(s) = \frac{G(s)}{1 + G(s)}=\frac{s+2}{s^3 + 5s^2 - 23s + 2}
$$


---

### (b) 상태변수 모델

상태변수 설정의 일관성을 위해 T(s) 분자, 분모에 Z(s)를 곱해준다.

$$
T(s) = \frac{Y(s)}{R(s)}=\frac{(s+2)Z(s)}{(s^3 + 5s^2 - 23s + 2)Z(s)}
$$

$$
Y(s) = (s+2)Z(s)
$$

이를 역라플라스 변환하면
$$
y(t) = \dot{z}(t) + 2z(t)
$$


$$
R(s) = (s^3 + 5s^2 - 23s + 2)Z(s)
$$

이를 역라플라스 변환하면

$$
r(t)=\dddot{z}(t) + 5\ddot{z}(t) -23\dot{z}(t) +2z(t)
$$

---

#### 상태변수 설정


$$
x(t) =
\begin{bmatrix}
x_1(t) \\
x_2(t) \\
x_3(t)
\end{bmatrix}
=
\begin{bmatrix}
z(t) \\
\dot{z}(t) \\
\ddot{z}(t)
\end{bmatrix}
$$

$$
x(t) = \begin{bmatrix}x_1(t) \\ x_2(t) \\ x_3(t)\end{bmatrix} = \begin{bmatrix}z(t) \\ \dot{z}(t) \\ \ddot{z}(t)\end{bmatrix}
$$


$$
\dot{x}_3(t) = \dddot{z}(t)
= r(t) - 5\ddot{z}(t) + 23\dot{z}(t) - 2z(t)
$$

따라서 상태방정식은

$$
\begin{cases}
\dot{x}_3(t) = -2x_1(t) + 23x_2(t) - 5x_3(t) + r(t) \\
\\[-2pt]
y(t) = 2x_1(t) + x_2(t)
\end{cases}
$$

---

#### 상태방정식 행렬형

$$
\dot{x}(t) =
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
-2 & 23 & -5
\end{bmatrix}
x(t)
+
\begin{bmatrix}
0 \\
0 \\
1
\end{bmatrix}
{r}(t)
$$

출력식:

$$
y(t) =
\begin{bmatrix}
2 & 1 & 0 \\
\end{bmatrix}
x(t)
$$

---

## P3.12 전달함수에서 상태방정식 구하기
### (a)

주어진 전달함수:

$$
T(s) = \frac{Y(s)}{R(s)} = \frac{8(s+5)z(s)}{(s^3 + 12s^2 + 44s + 48)z(s)}
$$

---

### (1) 각 항의 역라플라스 변환

$$
Y(s) = 8(s+5)z(s)
$$


$$
R(s) = s^3 + 12s^2 + 44s + 48)z(s)
$$

각각 라플라스 역변환을 해주면

$$
\begin{cases}
y(t) = 8\dot{z}(t) + 40z(t) \\[6pt]
r(t) = \dddot{z}(t) + 12\ddot{z}(t) + 44\dot{z}(t) + 48z(t)
\end{cases}
$$

---

### (2) 상태변수 정의

$$
x(t) = 
\begin{bmatrix}
x_1(t) \\
x_2(t) \\
x_3(t)
\end{bmatrix} =

\begin{bmatrix}
z(t) \\
\dot{z}(t) \\
\ddot{z}(t) 
\end{bmatrix} =

\begin{bmatrix} 
z(t) \\
\dot{x_1}(t) \\
\dot{x_2}(t) 
\end{bmatrix}






$$
x(t) =
\begin{bmatrix}
x_1(t) \\
x_2(t) \\[3pt]
x_3(t)
\end{bmatrix}
=
\begin{bmatrix}
z(t) \\[3pt]
\dot{z}(t) \\[3pt]
\ddot{z}(t)
\end{bmatrix}
$$


---

### (3) 상태방정식 도출

### 상태변수 방정식 (상태공간 모델)

$$
\begin{cases}
\dot{x}_3(t) = r(t) - 12\ddot{z}(t) - 44\dot{z}(t) - 48z(t) \\
y(t) = 8\dot{z}(t) + 40z(t)
\end{cases}
$$

---

$$
\begin{cases}
\dot{x}_3(t) = -48x_1(t) - 44x_2(t) - 12x_3(t) + r(t) \\
y(t) = 40x_1(t) + 8x_2(t)
\end{cases}
$$

---

### (4) 상태 미분 방정식

$$
\dot{x}(t) =
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
-48 & -44 & -12
\end{bmatrix}
x(t)
+
\begin{bmatrix}
0 \\
0 \\
1
\end{bmatrix}
r(t)
$$

$$
y(t) =
\begin{bmatrix}
40 & 8 & 0
\end{bmatrix}
x(t)
$$


---

### (b)

$$
A =
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
-48 & -44 & -12
\end{bmatrix}
$$

$$
\Phi(s) = [\, sI - A \,]^{-1}
$$

$$
\Phi(t) = \mathcal{L}^{-1} \Big\{ [\,sI - A\,]^{-1} \Big\}
$$

$$
[sI - A] =
\begin{bmatrix}
s & -1 & 0 \\
0 & s & -1 \\
48 & 44 & s+12
\end{bmatrix} =
임의의 행렬 x로 지정 후 matlab
$$

<img width="1412" height="476" alt="image" src="https://github.com/user-attachments/assets/3e31a92a-a09e-4277-8e55-3536b5bbb1af" />

따라서

$$
\Phi(t) =
\begin{bmatrix}
3e^{-2t} - 3e^{-4t} + e^{-6t} &
\frac{5}{4}e^{-2t} - 2e^{-4t} + \frac{3}{4}e^{-6t} &
\frac{1}{8}e^{-2t} - \frac{1}{4}e^{-4t} + \frac{1}{8}e^{-6t} \\
12e^{-4t} - 6e^{-2t} - 6e^{-6t} &
8e^{-4t} - \frac{5}{2}e^{-2t} - \frac{9}{2}e^{-6t} &
e^{-4t} - \frac{1}{4}e^{-2t} - \frac{3}{4}e^{-6t} \\
12e^{-2t} - 48e^{-4t} + 36e^{-6t} &
5e^{-2t} - 32e^{-4t} + 27e^{-6t} &
\frac{1}{2}e^{-2t} - 4e^{-4t} + \frac{9}{2}e^{-6t}
\end{bmatrix}
$$

## P3.17

행렬 \(A, B, C\) 는 다음과 같다:

$$
A =
\begin{bmatrix}
1 & 1 & -1 \\
4 & 3 & 0 \\
-2 & 1 & 0
\end{bmatrix},
\qquad
B =
\begin{bmatrix}
0 \\
0 \\
4
\end{bmatrix},
\qquad
C =
\begin{bmatrix}
1 & 0 & 0
\end{bmatrix}
$$

---

상태방정식은 다음과 같다:

$$
\begin{cases}
\dot{x}(t) = A\,x(t) + B\,u(t) \\
y(t) = C\,x(t)
\end{cases}
$$

$$
\left\{
\begin{aligned}
\dot{x}(t) &= A\,x(t) + B\,u(t) \\[6pt]
y(t) &= C\,x(t)
\end{aligned}
\right.
$$

$$ \dot{x}(t) = A\,x(t) + B\,u(t) $$
$$ y(t) = C\,x(t) $$



각각 라플라스 변환을 적용하면

$$
\begin{cases}
X(s) = [\,sI - A\,]^{-1} B\,U(s) \\[6pt]
Y(s) = C\,X(s)
\end{cases}
$$

두 식을 정리하면

$$
Y(s) = C\,\Phi(s)\,B\,U(s)
$$

$$
G(s) = \frac{Y(s)}{U(s)} = C\,\Phi(s)\,B
$$

따라서

$$
G(s) = \frac{12 - 4s}{s^3 - 14s^2 + 37s + 20}
$$

<img width="1110" height="1000" alt="image" src="https://github.com/user-attachments/assets/6f11cc73-dbea-4d1a-b484-9c9f09636fb4" />
