```cpp
//學號:1101444 姓名:徐英豈

/*
* 我宣告一個Person** 來創造n 個Person* 去對應到professor 或 student
set 做輸入的動作 我把name 跟 age 的cin 寫在virtual function 因為子類別都會輸入這兩個
所以我在進入子類別後呼叫Person 的virtual function 做完cin name跟age 後再個別輸入她想要的東西
*/

#include<iostream>
using namespace std;
#include <string>
class Person {
public:

	// 就算有東西也不會跑除非特別呼叫他 設成0 後為pure virtual不能宣告物件
	// 可以這樣寫
	//virtual void setData() = 0;
	//virtual void getData() = 0;

	virtual void setData() {
		cin >> name;
		cin >> age;
	}
	virtual void getData() {
		cout << name << ' ' << age << ' ';
	}

protected:
	string name = "";
	int age = 0;
};

class Professor :public Person {
public:
	void getData() {
		Person::getData();
		cout << publications <<' ' << 1 << endl;
	}
	void setData() {
		Person::setData();
		//cin >> name;
		//cin >> age;
		cin >> publications;
	}
private:
	int publications =0 ;
};

class Student :public Person {
public:
	void getData() {
		Person::getData();
		int tmp = 0;
		for (int i = 0; i < 6; ++i)
			tmp += marks[i];
		cout <<  tmp << ' '<< 2 << endl;
	}
	void setData() {
		Person::setData();
		//cin >> name >> age;
		for (int i = 0; i < 6; ++i) {
			cin >> marks[i];
		}

	}
private:
	int marks[6] = {};
};


int main() {
	int n, type;
	cout << "==========input==========" << endl;
	cin >> n;
	Person ** p = new Person*[n];
	for (int i = 0; i < n; ++i) {
		cin >> type;
		if (type == 1) {
			/* Professor tmp;
			p[i] = &tmp;*/
			p[i] = new Professor;
			p[i]->setData();
		}
		else {
			p[i] = new Student;
			p[i]->setData();
		/*	static Student tmp;
			p[i] = &tmp;*/
		}
	}
	cout << "==========output==========" << endl;
	for (int i = 0; i < n; ++i) {
		p[i]->getData();
	}
	return 0;
}

```
