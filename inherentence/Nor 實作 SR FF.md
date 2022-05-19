## 我的想法
```cpp
#include <iostream>
using namespace std;

class LogicGate {
protected:
	string label;
	bool output;
public:
	LogicGate(string label)
		: label(label),output(0) {
	}

	bool getOutput() {
		output = performGateLogic();
		return output;
	}

	virtual bool performGateLogic() {
		return true;
	}
	virtual void setNextPin(bool source) {}
};


class BinaryGate : public LogicGate {
protected:
	bool input1;
	bool input2;
	bool current;
public:
	BinaryGate(string label,bool b1,bool b2,bool cu) : LogicGate(label),input1(b1),input2(b2),current(cu) {}
};

class NorGate :public BinaryGate {
public:
	NorGate(string s, bool b1, bool b2, bool current) :BinaryGate(s, b1, b2, current) {}
	bool performGateLogic() {
		/*if (_b1 == 1 && _b2 == 1) {
		return
		}*/
		if (input1 == 0 && input2 == 0)
			return current;
		else if (input1 == 1)
			return true;
		else if (input2 == 1)
			return false;
	}

};
class SRgate :public LogicGate {
protected:
	bool input1;
	bool input2;
	bool current;
public:
	SRgate(string s, bool b1, bool b2, bool b3 = 0) :LogicGate(s),input1(b1),input2(b2),current(b3) {}

	bool performGateLogic() {
		cout << input1 << input2 << current;
		NorGate n1(label,input1,input2,current);
		return n1.performGateLogic();
	}
};

int main() {

	SRgate s1("SR", 0, 0);
	bool q1 = s1.getOutput();
	cout << " => " << q1 << endl;
	SRgate s2("SR", 0, 0, q1);
	bool q2 = s2.getOutput();
	cout << " => " << q2 << endl;
	
	SRgate s3("SR", 1, 0, q2);
	bool q3 = s3.getOutput();
	cout << " => " << q3 << endl;
	SRgate s4("SR", 0, 1, q3);
	bool q4 = s4.getOutput();
	cout << " => " << q4 << endl;;
	SRgate s5("SR", 0, 0, 1);
	bool q5 = s5.getOutput();
	cout << " => " << q5 << endl;
	return 0;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;
class LogicGate {
protected:
    string label;
    bool output;
public:
    LogicGate(string label)
        : label(label)
    {}

    bool getOutput() {
        output = performGateLogic();
        return output;
    }

    virtual bool performGateLogic() = 0;
    virtual void setNextPin(bool source) {}
};
class BinaryGate : public LogicGate {
protected:
    bool input1;
    bool input2;
    bool checkNext = true;
public:
    BinaryGate(string label = "") : LogicGate(label) {
    }
    void setNextPin(bool source) {
        if (checkNext) {
            input1 = source;
            checkNext = false;
        }
        else {
            input2 = source;
            //checkNext = true;
        }
    }
};
class NorGate :public BinaryGate {
public:
    bool performGateLogic() {
        return !(input1 || input2);
    }
};

class SRGate :public LogicGate {
    bool set, reset, Q;
    NorGate N1, N2;
public:
    SRGate(string label, bool s, bool res, bool q = 0)
        :LogicGate(label), set(s), reset(res), Q(q) {
    }
    bool performGateLogic() {
        N1.setNextPin(set);
        N1.setNextPin(Q);
        N2.setNextPin(reset);
        N2.setNextPin(N1.performGateLogic());
        cout << set << reset << Q;
        return N2.performGateLogic();
    }
};
int main() {
    SRGate s1("SR", 0, 0);
    bool q1 = s1.getOutput();
    cout << " => " << q1 << endl;

    SRGate s2("SR", 0, 0, q1);
    bool q2 = s2.getOutput();
    cout << " => " << q2 << endl;

    SRGate s3("SR", 1, 0, q2);
    bool q3 = s3.getOutput();
    cout << " => " << q3 << endl;

    SRGate s4("SR", 0, 1, q3);
    bool q4 = s4.getOutput();
    cout << " => " << q4 << endl;
	SRGate s5("SR", 0, 0, 1);
	bool q5 = s5.getOutput();
	cout << " => " << q5 << endl;

    return 0;
}
```
