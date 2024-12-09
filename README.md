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

#### 4.3.1. Xác định đáp ứng lối ra của hệ thống
```matlab
N = 10;
a = [1 -2]; % a_k
b = [1 -3]; % b_k
n = 0:N;
x = 2.^n; % Tín hiệu lối vào
x_in = filtic(b,a,1,0); % Giá trị khởi tạo
y = filter(b,a,x,x_in); % Đáp ứng lối ra
```


#### 5.2.1. Thiết kế cấu trúc tối ưu kiểu nối tiếp
```matlab
function [b0, B, A] = cautrucnoitiep(b, a)
    % Xác định nghiệm của tử số và mẫu số
    num_roots = cplxpair(roots(b)); % Nghiệm của tử số
    den_roots = cplxpair(roots(a)); % Nghiệm của mẫu số

    % Xử lý tử số
    if mod(length(num_roots), 2) ~= 0
        num_roots = [num_roots; 0]; % Bổ sung nghiệm 0 nếu số nghiệm là lẻ
    end
    
    B = []; % Ma trận chứa các đa thức bậc 2 từ nghiệm tử số
    for i = 1:2:length(num_roots)
        B = [B; poly(num_roots(i:i+1).')]; % Nhóm từng cặp nghiệm
    end

    % Xử lý mẫu số
    if mod(length(den_roots), 2) ~= 0
        den_roots = [den_roots; 0]; % Bổ sung nghiệm 0 nếu số nghiệm là lẻ
    end
    
    A = []; % Ma trận chứa các đa thức bậc 2 từ nghiệm mẫu số
    for i = 1:2:length(den_roots)
        A = [A; poly(den_roots(i:i+1).')]; % Nhóm từng cặp nghiệm
    end

    % Hệ số bậc 0 của tử số chia mẫu số
    b0 = b(1) / a(1);
end

```
