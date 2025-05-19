
# MATLAB & Python GNC Project

This project covers basic control system concepts using MATLAB and Python. It focuses on first-order and second-order systems, step response analysis, and closed-loop system behavior. The tasks aim to enhance understanding of system dynamics and transfer function modeling.

## Task 1: First-Order System - Varying Time Constant (T)

**System:**  
\[ G(s) = \frac{1}{Ts + 1} \]

**Objective:** Analyze unit step responses for different values of T.

### MATLAB Code
```matlab
T_values = [0.1, 0.5, 1.0, 5.0, 10.0];
t = 0:0.01:20;

figure;
hold on;
for T = T_values
    sys = tf(1, [T 1]);
    step(sys, t);
end
hold off;
legend('T=0.1','T=0.5','T=1.0','T=5.0','T=10.0');
title('Step Response for Different T');
xlabel('Time (s)'); ylabel('Amplitude');
grid on;
```

### Python Code
```python
import numpy as np
import matplotlib.pyplot as plt
from control import tf, step_response

T_values = [0.1, 0.5, 1.0, 5.0, 10.0]
t = np.linspace(0, 20, 1000)

plt.figure()
for T in T_values:
    sys = tf([1], [T, 1])
    t_out, y_out = step_response(sys, T=t)
    plt.plot(t_out, y_out, label=f'T={T}')

plt.legend()
plt.title('Step Response for Different T')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()
```

---

## Task 2: First-Order System - Varying Gain (k)

**System:**  
\[ G(s) = \frac{k}{s + 1} \]

### MATLAB Code
```matlab
k_values = [0.1, 0.5, 1.0, 5.0, 10.0];
t = 0:0.01:20;

figure;
hold on;
for k = k_values
    sys = tf(k, [1 1]);
    step(sys, t);
end
hold off;
legend('k=0.1','k=0.5','k=1.0','k=5.0','k=10.0');
title('Step Response for Different k');
xlabel('Time (s)'); ylabel('Amplitude');
grid on;
```

### Python Code
```python
k_values = [0.1, 0.5, 1.0, 5.0, 10.0]
t = np.linspace(0, 20, 1000)

plt.figure()
for k in k_values:
    sys = tf([k], [1, 1])
    t_out, y_out = step_response(sys, T=t)
    plt.plot(t_out, y_out, label=f'k={k}')

plt.legend()
plt.title('Step Response for Different k')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()
```

---

## Task 3: Second-Order System

**Differential Equation:**  
\[ \ddot{y} + 3\dot{y} + 2y = \dot{u} + 2u \]

### Transfer Function  
\[ G(s) = \frac{s + 2}{s^2 + 3s + 2} \]

### MATLAB Code
```matlab
numerator = [1 2];
denominator = [1 3 2];
sys = tf(numerator, denominator);

figure;
step(sys);
title('Second-Order System Step Response');
xlabel('Time (s)'); ylabel('Amplitude');
grid on;
```

### Python Code
```python
num = [1, 2]
den = [1, 3, 2]
sys = tf(num, den)

plt.figure()
t_out, y_out = step_response(sys)
plt.plot(t_out, y_out)
plt.title('Second-Order System Step Response')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()
```

---

## Task 4: Interpretation of Code

```matlab
g = tf([10 0], [1 10 25]);
```

Defines:  
\[ G(s) = \frac{10s}{s^2 + 10s + 25} \]  
A second-order system with a zero at the origin.

---

## Task 5: Closed-Loop System

**Given:**  
- G(s) = 1 / (s + 2)  
- H(s) = 2 / (s + 3)

### MATLAB Code
```matlab
G = tf(1, [1 2]);
H = tf(2, [1 3]);
open_loop = series(G, H);
closed_loop = feedback(open_loop, 1);

figure;
step(closed_loop);
title('Closed-Loop Step Response');
xlabel('Time (s)'); ylabel('Amplitude');
grid on;

final_value = dcgain(closed_loop);
disp(['Final value: ', num2str(final_value)]);
```

### Python Code
```python
from control import tf, step_response, feedback, dcgain
import matplotlib.pyplot as plt
import numpy as np

# Define G(s) and H(s)
G = tf([1], [1, 2])
H = tf([2], [1, 3])

# Create closed-loop system with H(s) in feedback
closed_loop = feedback(G, H)

# Step response
t_out, y_out = step_response(closed_loop)

# Plotting
plt.figure()
plt.plot(t_out, y_out)
plt.title('Closed-Loop Step Response')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')
plt.grid(True)
plt.show()

# Final value
print("Final value:", dcgain(closed_loop))
```

---

## Useful Resources

- YouTube:
  - [First-Order Step Response](https://www.youtube.com/watch?v=dYf0g_1lN8k)
  - [Second-Order Step Response](https://www.youtube.com/watch?v=RfjQeS7sOWk)
- MATLAB Docs: [Step Response](https://www.mathworks.com/help/control/ref/dynamicsystem.step.html)
- GitHub: Search for `matlab control systems` or `python control step response`

---

## Conclusion

This project provides foundational insight into control systems using MATLAB and Python. Feel free to experiment by modifying system parameters and analyzing the effects on system dynamics.
