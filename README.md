# Xử lý tín hiệu số

## Chương 4
#### 4.2.1. Tính chất của hệ thống
- Kiểm tra tính ổn định của hệ thống
```matlab
% Khai báo hệ thống
numerator = 4; % Tử số của H(z)
denominator = [1 2 10]; % Mẫu số của H(z)
Ts = 0.1; % Thời gian lấy mẫu
H = tf(numerator,denominator,Ts);

% Tính đáp ứng xung
h = impulse(H);

% Tính tổng năng lượng
E = sum(h.^2);

if isfinite(E)
    disp("Hệ thống ổn định");
else
    disp("Hệ thống không ổn định");
end
```
