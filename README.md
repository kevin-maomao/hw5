# Hw5
# PwmOut and logic analyzer

copy from github https://github.com/ARMmbed/mbed-os-snippet-PwmOut_ex_3
and modify the code referencing breathing light
createe an object breathingLight and use eventqueue to simutaneously observe the PWM

## Codes modified in main.cpp

```python
class breathingLight {
public:
    breathingLight(PwmOut &pwm, events::EventQueue &event_queue, float duty = 0): pwm(pwm), _event_queue(event_queue), duty(duty){
        printf("Init\n");
    }
    void start(){
        pwm.period(0.005f);
        pwm.write(duty);
        _event_queue.call(
            [this] {
                updateLight();
            }
        );
        _event_queue.dispatch_forever();
    }
private:
    void updateLight(){
        while (1) {
            // printf("Update: %f\n", duty);
            if(duty>=1){
                isReverse = true;
            }
            if(duty<0){
                isReverse = false;
            }
            isReverse?(duty-=0.05):(duty+=0.05);
            pwm.write(duty);
            wait_us(10000);
        }
    }
    PwmOut &pwm;
    float duty;
    bool isReverse = false;
    events::EventQueue &_event_queue;
};
```

```python
int main()
{
    breathingLight breathLed = breathingLight(led, event_queue);
    breathingLight breathBoardLed = breathingLight(ledboard, event_queue);
    
    breathLed.start();
    breathBoardLed.start();
    
    while (1);
}
```

Observing PWM using logic analyzer

![螢幕擷取畫面 2023-04-20 170303](https://user-images.githubusercontent.com/59012686/233316420-f11cf2f3-cefe-437f-888e-73111a0e86fd.png)
