# hw5
# PwmOut and logic analyzer

copy from github https://github.com/ARMmbed/mbed-os-snippet-PwmOut_ex_3

## Codes modified in main.cpp

```python
PwmOut led(PWM_OUT);

int main()
{
    // specify period first
    led.period(0.05f);      // 0.05 second period
    led.write(0.50f);      // 50% duty cycle, relative to period
    //led = 0.5f;          // shorthand for led.write()
    //led.pulsewidth(2);   // alternative to led.write, set duty cycle time in seconds
    while (1);
}
```

Observing PWM using logic analyzer

![螢幕擷取畫面 2023-04-20 170303](https://user-images.githubusercontent.com/59012686/233316420-f11cf2f3-cefe-437f-888e-73111a0e86fd.png)
