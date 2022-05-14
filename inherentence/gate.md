```cpp
#include <iostream>
using namespace std;
#include <string>

class LogicGate {
public:
	LogicGate(string s) {
		label = s;
	}
	void getoutput() {
		cout << "output : " << output << endl << endl;
	}

protected:
	string label;
	bool gate1;
	bool gate2;
	bool output;
};


class BinaryGate :public LogicGate {
public:
	BinaryGate(string s) :LogicGate(s) {
		set();
	}
	void set();
};

void BinaryGate::set() {
	cout << "Enter pin input for gate " << label << ": ";
	cin >> gate1;
	cout << "Enter pin input for gate " << label << ": ";
	cin >> gate2;
}

class UnaryGate :public LogicGate {
public:
	UnaryGate(string s) :LogicGate(s) {
		set();
	}
	void set();
};
void UnaryGate::set() {
	cout << "Enter pin input for gate " << label << ": ";
	cin >> gate1;
}

class ANDgate :public BinaryGate {
public:
	ANDgate(string s = "") :BinaryGate(s) {
		if (gate1 && gate2)
			output = true;
		else
			output = false;
		getoutput();
	}
};


class ORgate :public BinaryGate {
public:
	ORgate(string s) :BinaryGate(s) {
		if (gate1 || gate2)
			output = true;
		else
			output = false;
		getoutput();
	}
};

class NOTgate :public UnaryGate {
public:
	NOTgate(string s) :UnaryGate(s) {
		if (gate1)
			output = false;
		else
			output = true;
		getoutput();
	}
};

int main() {

	string s;
	while (cin >> s) {
		if (s == "and") {
			ANDgate test(s);
		}
		else if (s == "or") {
			ORgate test2(s);
		}
		else if (s == "not") {
			NOTgate test3(s);
		}
	}

	return 0;
}
```
