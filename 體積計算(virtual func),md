```cpp
#include <iostream>
using namespace std;
#include <cmath>
//volume
class Shape {
public:
	virtual void get_size() = 0;
	
protected:
	int size;
};
//x y
class Point {
public:
	int x, y;
	Point(int a, int b) {
		x = a;
		y = b;
	}
};


int distance(Point a, Point b) {
	return sqrt(pow(a.x - b.x, 2) + pow(a.y - b.y, 2));
}

//area
class Square {
public:
	void square_area(Point a,Point b) {
		 squareArea = pow(distance(a,b),2);
	}
protected:
	int squareArea;

};
//area
class Circle {
public:
	void circle_area(Point a, Point b) {
		circleArea = pow(distance(a,b) ,2) * 3.14;
	}
	
protected:
	int circleArea;
};
//立方體
class Cube :public Square, public Shape {

public:
	Cube(Point a,Point b,Point c) {
		cout << "Cube : ";

		size = squareArea*distance(a,c);
		 
	}
	void get_size() {
		cout << size;
	}
	

};
//圓柱體
class Cylinder :public Circle, public Shape {
public:

	Cylinder(Point a, Point b, Point c) {
		cout<< "Cylinder : ";
		size = circleArea * distance(a, c);

	}
	void get_size() {
		cout << size;
	}

};


int main() {

	Cube cube(Point(0, 0), Point(0, 5), Point(5, 0));
	Shape* s1 = &cube;
	s1->get_size();
	cout << endl;

	Cylinder cylinder(Point(0, 0), Point(0, 5), Point(5, 0));
	Shape* s2 = &cylinder;
	s2->get_size();
	cout << endl;


	return 0;
}
```
