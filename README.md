# 💡 Experiment 01 – Interfacing a Digital Output (LED) with ARM Development Board

### 🎯 **Aim**
To interface a digital output (LED) to an ARM development board and write a blink code.

---

### ⚙️ **Components Required**
- STM32CubeIDE  
- NUCLEO ARM Development Board  

---

### 🧠 **Theory**

**ARM (Advanced RISC Machine)** is a 32-bit processor architecture developed by ARM Holdings. It is widely used in embedded systems and SoC (System-on-Chip) products. Many semiconductor companies like Samsung, Atmel, and Texas Instruments license ARM architecture to design their own SoCs.
### 🧩 **What is an ARM7 Processor?**
The **ARM7 processor** is commonly used in embedded system applications. It provides a balance between the classic ARM architecture and the newer Cortex series, offering an excellent platform for both hardware and software development.
### 🔍 **LPC2148 Microcontroller**
The **LPC2148**, developed by NXP Semiconductors (Philips), is a 16/32-bit ARM7-based microcontroller featuring a wide range of peripherals.
#### **Key Features**
- 16/32-bit ARM7TDMI-S core in LQFP64 package  
- On-chip **Flash memory**: 32 KB – 512 KB  
- On-chip **SRAM**: 8 KB – 40 KB  
- **ISP/IAP** via on-chip bootloader  
- **Embedded ICE-RT** and **Real Monitor** for real-time debugging  
- **USB 2.0** full-speed device controller with 2 KB endpoint RAM  
- **10-bit ADC** (6 or 14 channels, 2.44 μs conversion time)  
- **10-bit DAC** for analog output  
- **Timers:** Two 32-bit timers, watchdog, and PWM unit  
- **RTC** with 32 kHz clock input  
- **UARTs (2x), I²C (2x)** up to 400 kbit/s  
- **5V-tolerant GPIOs**, 21 external interrupt pins  
- **Max CPU Clock:** 60 MHz using on-chip PLL (lock time 100 µs)  
- **Crystal Frequency:** 1 MHz – 25 MHz  
- **Power modes:** Idle and Power-down with peripheral clock scaling  

---

### 🧭 **Procedure**

1. Open **STM32CubeIDE**.
  <img width="1907" height="1061" alt="Screenshot 2025-10-28 193741" src="https://github.com/user-attachments/assets/34534b43-34ec-4849-bb55-a3adcefc2b2e" />



2. Click **File → New STM32 Project**.
   <img width="1920" height="1080" alt="Screenshot 2025-10-28 194000" src="https://github.com/user-attachments/assets/a6798175-554a-44f1-861e-8a05027977e9" />
   <img width="1914" height="1080" alt="Screenshot 2025-10-28 194116" src="https://github.com/user-attachments/assets/1a1783d8-6525-40c6-b99b-8a3fef5418cc" />

   
3.Select the target microcontroller or board and click Next.
<img width="1920" height="1080" alt="Screenshot 2025-10-28 195546" src="https://github.com/user-attachments/assets/d4b3398f-13a8-419b-9830-a8d3cf639597" />


4. Name the project.
<img width="1919" height="1080" alt="{F0C19B8A-3D31-4246-AFCA-090D826C21C6}" src="https://github.com/user-attachments/assets/eb381a86-584f-4fc1-88ac-9ca1e439384f" />



5. Select the **target microcontroller** or board and click **Next**.
<img width="1920" height="1080" alt="{A6441063-5972-4309-8C83-5D3060326888}" src="https://github.com/user-attachments/assets/5fbdf625-2d86-41ab-8145-5deab8193102" />




6. The corresponding `.ioc` file will be generated automatically.
<img width="1920" height="1080" alt="{E4EFEAEE-460A-4069-B3DB-6931BF3FB3D4}" src="https://github.com/user-attachments/assets/3cfade26-7d0d-4458-9125-ddc0feaf688b" />



7. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
   <img width="1920" height="1080" alt="{7479B8B5-FC96-452A-9AFE-A9A942D0B0EB}" src="https://github.com/user-attachments/assets/afee08f0-6877-4d4d-a7ea-66cdf4bb4040" />



8. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
<img width="1920" height="1079" alt="{3D0A08CF-9BBB-461C-9E1C-CB5ED8791C1B}" src="https://github.com/user-attachments/assets/fd2cd272-725b-4c2b-8d87-05aa1522c3a0" />

<img width="1915" height="1080" alt="{1580E531-1D73-4731-9628-0FD38E9C4523}" src="https://github.com/user-attachments/assets/d84461e7-f460-4376-ad4a-c18cfe655ce8" />


 
9. Edit the generated main program as required.
<img width="984" height="408" alt="Screenshot 2025-10-28 205257" src="https://github.com/user-attachments/assets/5d8735b7-fb1f-491e-87db-80e7ea801bc3" />



10. Click **Project → Build All**.
    <img width="1920" height="895" alt="{2B360418-D9D7-443D-BEEB-2334AB05EFDE}" src="https://github.com/user-attachments/assets/8bbfe3d9-68d5-4d91-9a83-957621d11c19" />




11. Link the **HEX file** using the post-build process.
 <img width="742" height="266" alt="{C5DB54B9-26B5-41EE-8F1D-B7C00195EA1C}" src="https://github.com/user-attachments/assets/28ec5c3c-0866-4712-ba93-81d971862e07" />




12. Click **Debug** and connect the **STM Nucleo Board**.
<img width="1920" height="1080" alt="{25ECC312-2989-45C3-A9F0-E8B65ED3AA12}" src="https://github.com/user-attachments/assets/ffc7c7ee-a375-4475-b700-168835489bb6" />



13. Click **Run** to execute the program.
### 💻 **Program**
```
#include "main.h"
void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

   while (1)
    {
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);
        HAL_Delay(1000);
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
        HAL_Delay(1000);
    }
}
```

### OUTPUT
CASE 1: LED ON 
![WhatsApp Image 2025-10-27 at 20 12 54_b43d1f17](https://github.com/user-attachments/assets/e0c3f403-c6ee-44ff-a111-06814bfc53a2)


CASE 2: LED OFF
![WhatsApp Image 2025-10-27 at 20 12 54_15886613](https://github.com/user-attachments/assets/45947529-b89c-4d5a-ba28-9ec93989710d)



---
### RESULT
Interfacing a digital output with ARM microcontroller is executed and the results are verified.
