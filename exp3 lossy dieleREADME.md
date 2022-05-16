% Lossy dielectric (germanium)
clear all;
close all;
clc;
c = 3 * 10.^ 8; % speed of light
w = 10.^8; % angular frequency of wave
mu = 1 *4* pi *10.^(-7); % Permeability
epsilon = 4 * 8.854 * 10.^(-12); %permittivity
sigma = 0.64; % conductivity
k = (mu * epsilon)/ 2;
alpha = w*(sqrt(k *(sqrt(1 + (sigma/(w*epsilon)).^2)-1))); % attenuation constant
beta = w*(sqrt(k *(sqrt(1 + (sigma/(w*epsilon)).^2)+1))); % phase constant
ita = (sqrt(mu/epsilon))/(1 + (sigma/(w*epsilon)).^2).^(0.25); % intrinsic impedance
theta = 0.5 * atan(sigma/(w*epsilon));
t = -0.5:0.01:0.5;
x = -0.5:0.01:0.5;
m = zeros(size(t));
Ey = 30*cos(w*t - beta *x).*exp(-alpha*x);
Hz = (30/ita)*cos(w*t - beta*x - theta).*exp(-alpha*x);
figure(1);
plot3(x,Ey,m,'r');
hold on;
t = -0.5:0.01:0.5;
plot3(x,m,Hz,'blue');
grid on;
hold off;
ylabel('Electric Field');
zlabel('Magnetic Field');
xlabel('Direction of Wave');
title('Em Wave components in Lossy Dielectric Medium');
view(10,10);
