# FIR-Filter-Design-Analysis
FIR Filter Design &amp; Analysis (MATLAB) This project demonstrates the design and analysis of a low‑pass FIR filter using the window method (Hamming window) in MATLAB. It includes Filter design parameters. Implementation of FIR filter using fir1 with Hamming window.  Signal generation.  Application of the filter to remove high‑frequency noise.
// MATLAB CODE 
% FIR Filter Design & Analysis
% Low-pass Filter using Window method
clear; close all; clc;

% Parameters
Fs = 1000;   % Sampling frequency (Hz)
Fc = 100;    % Cutoff frequency (Hz)
N = 60;      % Filter order
wc = Fc / (Fs/2); % Normalized cutoff frequency (0 to 1)

% Design FIR filter using Hamming window
b = fir1(N, wc, 'low', hamming(N+1));
[h, w] = freqz(b, 1, 1024, Fs);

% Impulse response
n = 0:N;
imp = [1 zeros(1,100)];
step_resp = filter(b,1,ones(1,100)); % Correct step response

% Generate test signal
t = 0:1/Fs:1;
x = sin(2*pi*15*t) + 0.5*sin(2*pi*200*t); % Original signal
y = filter(b,1,x); % Filtered signal

% Plotting
figure(1);
freqz(b,1,1024,Fs); grid on;
title('Magnitude Response of FIR Low-pass Filter');

figure(2);
stem(n,b,'LineWidth',1.5); grid on;
title('Impulse Response of FIR Filter');
xlabel('Samples'); ylabel('Amplitude');

figure(3);
plot(t,x,'r',t,y,'b','LineWidth',1.2); grid on;
title('Time Domain Signal: Before & After Filtering');
legend('Original Signal','Filtered Signal');
xlabel('Time (s)'); ylabel('Amplitude');

figure(4);
plot(w,20*log10(abs(h)),'LineWidth',1.5); grid on;
title('Magnitude Response in dB');
xlabel('Frequency (Hz)'); ylabel('Magnitude (dB)');

figure(5);
plot(w,unwrap(angle(h)),'LineWidth',1.5); grid on;
title('Phase Response');
xlabel('Frequency (Hz)'); ylabel('Phase (radians)');

figure(6);
plot(step_resp,'LineWidth',1.5); grid on;
title('Step Response of FIR Filter');
xlabel('Samples'); ylabel('Amplitude');
gtext('Pranav Parasar');
<img width="1402" height="1122" alt="image" src="https://github.com/user-attachments/assets/40effa28-ec06-443a-95c7-6a3c0e02ece7" />
