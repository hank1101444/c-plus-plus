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
