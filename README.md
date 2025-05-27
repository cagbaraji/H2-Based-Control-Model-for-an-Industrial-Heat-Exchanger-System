# H2-Based-Control-Model-for-an-Industrial-Heat-Exchanger-System

Heat Exchangers, also called circulation heaters, are used to circulate specific heat in a system without direct contact between the source and the heated medium. Heat exchanger is commonly used in industrial processes to transfer heat from the hot fluid through a solid wall to a cooler fluid. 

The robust control strategies design for industrial thermal systems is very vital most especially to ensure stability, optimal efficiency, and safety industrial processes. Heat exchanger is one of the systems that play a critical role in the process of thermal energy transfer between fluids, in most instances under varying operating conditions or uncertainties and disturbances from many sources. 

The control of heat exchanger is a difficult issue to achieve because of the time delay parameter involved in the plant model which is experienced practically when thermal energy is being transferred between fluids. As a result, traditional control methods such as PID may fail to maintain good performance and stability in the presence of significant disturbances. In this case, a robust control is required to handle the level of uncertainties that exist in such systems. 
This study focuses on the development of a H2 syntheses-based controller for the heat exchanger using MATLAB. The H2 synthesis controller is a modern control strategy that optimizes system performance by minimizing the H2 norm, which relates to the amplification of energy from disturbances to output. 

The objectives of this work is to design a H2 synthesis-based robust controller that can deliver optimal performance and disturbance rejection, and also maintain robust stability across a range of operating conditions and disturbances. 

### Plant Model
The transfer function of the shell and tube heat exchanger was derived in (Sivakumar et al, 2012) and described as the nth-order with pure time delay, expressed as follows:

![image](https://github.com/user-attachments/assets/f8db8946-c466-41df-9664-2cabf5d511fe)

Let ![image](https://github.com/user-attachments/assets/7660f8a1-f6a1-43c0-b7b6-4217bec73594)

![image](https://github.com/user-attachments/assets/8b557a5a-26d5-4b6f-9096-088a69d56683)

![image](https://github.com/user-attachments/assets/1359cc8d-7875-46d9-968e-78d1933ca2b2)

where
L is the distance of the pipeline 

V is the velocity of the fluid through the pipeline

![image](https://github.com/user-attachments/assets/75bbaf80-74ce-42ae-a7a2-c4a25f014cd3) is the temperature of output fluid

![image](https://github.com/user-attachments/assets/19e2aac8-e8da-48c0-a479-bc9129bc70c2) is the temperature of the input fluid

![image](https://github.com/user-attachments/assets/0de36dc6-4d50-4660-bba5-f1ee0f343096)

![image](https://github.com/user-attachments/assets/b64abf62-2ac2-41ec-8d26-bb465adc65c0)

where r, K and D refer to time constant, system gain, and delay time respectively.

Table 1: Process parameters (Vasickaninova and Bakosova, 2013)

![image](https://github.com/user-attachments/assets/740b2c06-c19e-415a-85ce-2ad88f66cbf4)

### Control Mechanism
Figure 1 illustrates the application of a feedback mechanism to the heat exchanger plant in order to enhance performance (such as tracking error and sensitivity to disturbance) and stability. An error e(t), which varies over time, is produced when the measured actual output of the heat exchanger is compared to the reference input into the system. The error signal time variation makes it challenging to control in order to generate a control signal that will be supplied into the fixed plant to improve stability and performance.

![image](https://github.com/user-attachments/assets/6273b843-4e1b-42df-a2c0-be89c21e312e)

Figure 1: Controlled heat exchanger plant

In practice the heat exchanger like other physical systems ystem has disturbance sources or faults and noise that affect the system performance as illustrated in figure 2. 

![image](https://github.com/user-attachments/assets/eccdc7ed-1d62-403e-bde7-18c9c4d86f15)

Figure 2: Controlled Heat exchanger plant with disturbance and noise inputs

In practice, the inputs into the heat exchanger controlled plant become:

![image](https://github.com/user-attachments/assets/9233e184-4171-426d-9e35-c3abb3c637b3) = Reference input

![image](https://github.com/user-attachments/assets/b631635b-e99d-4157-b48a-8ffa757bcafd) = Disturbance input

![image](https://github.com/user-attachments/assets/299ab2fc-d9d8-4d22-8985-4379f6a5c8a3) = Noise input

The actual output when all the inputs are considered in the heat exchanger controlled plant gives:

![image](https://github.com/user-attachments/assets/7deb952b-cd4a-4fa2-a38a-a38bec0831e3)

### Applying H2 Synthesis

The H2 controller design method here involves the control of the tracking performance of the heat exchanger and it’s stability with the H2 weights W1 and W2 based on the heat exchanger parameters. The weight parameters are varied randomly in order to improve the iteration results and to improve the performance graph trajectory. The weighting functions were chosen based on the industrial performance specifications for H2 and H-Infinity weights in (Filardi et al):
Wp (W1): the inverse of the weighting function Wp(s) is used to impose a performance specification in terms of the sensitivity function S. Wp is chosen:

![image](https://github.com/user-attachments/assets/d3aec4b6-eec9-487d-a417-430e3e6bdf7c)

Where Ms is to introduce a margin of robustness on the peak of S, wb helps to have a sensible attenuation of disturbances and As helps to reduce the steady-state performance tracking error.

Wu (W2): the control output u is weighted according to the actuator limitations. Wu(s) is set to:

![image](https://github.com/user-attachments/assets/8a1f237a-7e43-422d-b408-c311220cc77b)

Where Mu helps to impose limitations on the maximum value of the controller output signal, wbc helps to limit the effect of measurement noise and plant uncertainties at high frequencies, and ε helps to ensure a high-frequency controller gain.

The H2 control algorithm can be presented as follows:

i.	Apply the heat exchanger model 

![image](https://github.com/user-attachments/assets/4141654f-407e-4e6e-b2fb-2a5ad3a4565b)

ii.	Apply weight W1 to control the plant sensitivity to disturbance

iii.	Apply Weight W2 on the control signal u

iv.	Augment the plant G(s) with weighting functions W1(s) and W2(s) to form an “augmented plant” P(s)

v.	Apply H2 synthesis and generate the controller K1 

vi.	Compute the loop gain L:

![image](https://github.com/user-attachments/assets/6237f79b-21e6-40b4-91e5-460b3a0bbd32)

![image](https://github.com/user-attachments/assets/2df5d15a-cb2b-479d-8d2c-87543a7112d1)

![image](https://github.com/user-attachments/assets/1aad6915-734c-4273-ac01-f987ae36ec1a)

vii.	Develop the system sensitivity function 

![image](https://github.com/user-attachments/assets/59c0acb8-6325-4f2d-adcf-b1fb6326b9f1)

![image](https://github.com/user-attachments/assets/55dd6cfe-f147-4777-acea-11a252ff0bec)

![image](https://github.com/user-attachments/assets/9aac9d3e-68f4-4d70-bdbe-bcdc4950e249)

![image](https://github.com/user-attachments/assets/2125c677-c578-4a59-988f-416fff30e53e)

![image](https://github.com/user-attachments/assets/e0d60f43-97c2-43ae-a33c-692749f86010)

viii.	        Compute the complementary sensitivity function T:

![image](https://github.com/user-attachments/assets/299d92a6-24eb-4eaa-be9e-7fb4d49811d3)

![image](https://github.com/user-attachments/assets/8d474702-a24e-43bb-87ad-62f8b5dec9ba)

![image](https://github.com/user-attachments/assets/00fc4382-875a-4019-9039-e3094953f2d3)

![image](https://github.com/user-attachments/assets/112a46b8-8e19-4830-b1ee-8f9654d19ab4)

ix.	Analyze L, S and T for performance tracking and stability for the heat exchanger

This method of controller design allows very precise loop shaping through suitable weighting strategies and thereby achieves improved performance tracking. Augmenting the plant with frequency dependent weights W1 and W2, the MATLAB script h2syn will find a controller that shapes the signals to achieve the desired performance of the system. The MATLAB function aug forms the augmented plant function. 

### Results

![image](https://github.com/user-attachments/assets/b29e870b-b556-4ee1-affd-80f6bf3d9eee)

Figure 3: Loop gain bode plot analysis when D=0 and k=0.1

![image](https://github.com/user-attachments/assets/0529f786-18c8-47b2-b1ae-5f684241e878)

Figure 4: Loop gain Nyquist plot analysis when D=0 and k=1

![image](https://github.com/user-attachments/assets/dd347f63-079f-47c1-a7d6-4861ec479699)

Figure 5: T, S and L graphs for the system for the minimum value simulation

The state space model of the controller K1, was achieved for the minimum value simulation as follows:

![image](https://github.com/user-attachments/assets/0fa6aa76-bdb1-4bae-b74d-6b2e94c44624)

![image](https://github.com/user-attachments/assets/bf2d251b-10fe-44ee-9ea9-5069ffeb95eb)

![image](https://github.com/user-attachments/assets/959ffe4a-6c87-4345-9546-96673d635af8)

### Validation of Results

![image](https://github.com/user-attachments/assets/2a054aef-178b-4328-820e-ae8f02c4af8a)

Figure 6: Step response graph of the system for the minimum value simulation

![image](https://github.com/user-attachments/assets/81a69eba-3e5e-4d52-a308-c3503521abf7)

Figure 7: Bode plot of the system for the minimum value simulation




