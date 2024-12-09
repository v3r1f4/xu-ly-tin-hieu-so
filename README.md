# Xử lý tín hiệu số

## Chương 2
#### 2.2.2. Phép toán phụ thuộc vào biến thời gian
- Tích chập
```matlab
function [y, n] = sig_conv(a,na,b,nb)
y = conv(a,b);
n1 = na(1) + nb(1);
n2 = na(end) + nb(end);
n = n1:n2;
```

## Chương 4
#### 4.2.1. Tính chất của hệ thống
- Kiểm tra tính nhân quả và ổn định của hệ thống
```matlab
% Khai báo hệ thống
numerator = 4; % Tử số của H(z)
denominator = [1 2 10]; % Mẫu số của H(z)
Ts = 0.1; % Thời gian lấy mẫu
H = tf(numerator,denominator,Ts);

% Tính đáp ứng xung
[h, t] = impulse(H);

% Tính tổng năng lượng
E = sum(h.^2);

if all(h(t < 0) == 0)
    disp("Hệ thống nhân quả");
else
    disp("Hệ thống không ổn định");
end

if isfinite(E)
    disp("Hệ thống ổn định");
else
    disp("Hệ thống không ổn định");
end

```
