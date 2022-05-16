h=0.01;
vo=1;
a=2.0;
b=a;
c=4*vo/pi;
IMAX = a/h;
JMAX = b/h;
NMAX = 11;
for I=1:IMAX
x=h*I;
for J=1:JMAX
y=h*J;
sum=0.0;
for n =1:2:NMAX
a1=sin(n*pi*x/b);
a2=sinh(n*pi*y/b);
a3=n*sinh(n*pi*a/b);
sum= sum + c*a1*a2/a3;
end
V(J,I)=sum;
end
end
[xmesh,ymesh] = meshgrid(1:IMAX ,1:JMAX);
mesh(V);
xlabel('x(cm)');
ylabel('y(cm)');
zlabel('Voltage(V)')
title('Voltage at any point (x, y)');
figure;
[C,h] = contour(xmesh,ymesh,V);
set(h,'ShowText','on','TextStep',get(h,'LevelStep'));
xlabel('x(cm)');
ylabel('y(cm)');
title('Contour of the Voltage ');
figure;
contour(xmesh,ymesh,V); [px,py] = gradient(V);
hold on,quiver(xmesh,ymesh,-px,-py,5),hold off,
xlabel('x(cm)');
ylabel('y(cm)');
title('Electric Field Lines ');
