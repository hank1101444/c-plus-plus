```cpp
#include <iostream>
using namespace std;
#include <string>

class LogicGate {
public:
	LogicGate(string s) {
		label = s;
	}

	virtual bool performGateLogic() {};
	virtual void setNextPin(bool source) {};
	bool getoutput() {
		//cout << "output : " << output << endl << endl;
		output = performGateLogic();
		return output;
	}

protected:
	string label;
	bool  gate1;
	bool gate2;
	bool flag = true;
	bool output;
};

class Connector {
	LogicGate* fromgate, * togate;
	Connector(LogicGate* fgate, LogicGate* tgate) {
		fromgate = fgate;
		togate = tgate;
		tgate->setNextPin(fromgate->getoutput());
	}
};


class BinaryGate :public LogicGate {
public:
	BinaryGate(string s) :LogicGate(s) {
		
	}
	void setNextPin(bool source) {
		if (flag) {
			gate1 = source;
			flag = false;
		}
		else
			gate2 = source;
	};
	
};
//
//void BinaryGate::set() {
//	cout << "Enter pin input for gate " << label << ": ";
//	cin >> gate1;
//	cout << "Enter pin input for gate " << label << ": ";
//	cin >> gate2;
//}

class UnaryGate :public LogicGate {
public:
	UnaryGate(string s) :LogicGate(s) {
	}
	void setNextPin(bool source) {
		if (flag) {
			gate1 = source;
			flag = false;
		}
		else
			gate2 = source;
	};
};


class ANDgate :public BinaryGate {
public:
	ANDgate(string s = "") :BinaryGate(s) {
	}
	bool performGateLogic() {
		if (gate1 && gate2)
			output = 1;
		else
			output = 0;
		return output;
	}
};


class ORgate :public BinaryGate {
public:
	ORgate(string s) :BinaryGate(s) {
	}
	bool performGateLogic() {
		if (gate1 && gate2)
			output = 1;
		else
			output = 0;
		return output;
	}
};

class NOTgate :public UnaryGate {
public:
	NOTgate(string s) :UnaryGate(s) {
	}
	bool performGateLogic() {
		if (gate1 == true)
			output = false;
		else
			output = false;
		return output;
	}
};

int main() {

	ANDgate g1("A");
	g1.setNextPin(1);
	g1.setNextPin(0);


	return 0;
}
```
