clear all;
close all;
clc;
c = 3 * 10.^ 8; % speed of light
w = 10.^8; % angular frequency of wave
beta = w/c; % Phase constant
t = -0.5:0.01:0.5; % time
x = -0.5:0.01:0.5; % space (direction of propogation)
m = zeros(size(t));
Ey = 30*cos(w*t - beta *x);% electric field
Hz = (30/377)*cos(w*t - beta*x);% magnetic field
figure(1);
plot3(x,Ey,m,'r'); % Plotting 3d electrical wave
hold on;
t = -0.5:0.01:0.5;
plot3(x,m,Hz,'g');% Plotting 3d magnetic wave
grid on;
hold off;
ylabel('Electric Field');
zlabel('Magnetic Field');
xlabel('Direction of Wave');
title('Em Wave components in Free Space Medium');
view(10,10)
