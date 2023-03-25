# EXPERIMENT--02-INTERFACEING-A-DIGITAL-INPUT-TO-IOT-DEVELOPMENT-BOARD-
 

## Aim: To Interface a Digital Input  (IR pair ) to ARM IOT development board and write a  program to obtain  the data 
## Components required: STM32 CUBE IDE, ARM IOT development board,  STM programmer tool.
## Theory 
The full form of an ARM is an advanced reduced instruction set computer (RISC) machine, and it is a 32-bit processor architecture expanded by ARM holdings. The applications of an ARM processor include several microcontrollers as well as processors. The architecture of an ARM processor was licensed by many corporations for designing ARM processor-based SoC products and CPUs. This allows the corporations to manufacture their products using ARM architecture. Likewise, all main semiconductor companies will make ARM-based SOCs such as Samsung, Atmel, TI etc.

 
 # IR pair 
 
 ![image](https://user-images.githubusercontent.com/36288975/227598600-730748bf-9884-4a33-95bf-a1fbfde518ed.png)

 IR technology is used in a wide range of wireless applications which includes remote controls and sensing. The infrared part in the electromagnetic spectrum can be separated into three main regions: near IR, mid-IR & far IR. The wavelengths of these three regions vary based on the application. For the near IR region, the wavelength ranges from 700 nm- 1400 nm, the wavelength of the mid-IR region ranges from 1400 nm – 3000 nm & finally for the far IR region, the wavelength ranges from 3000 nm – 1 mm.The near IR region is used on fiber optic & IR sensors, the mid-IR region is used for heat sensing and the far IR region is used in thermal imaging. The range of frequency for IR is maximum as compared to microwave and minimum than visible light.  
## Procedure:
 1. click on STM 32 CUBE IDE, the following screen will appear 
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)

 2. click on FILE, click on new stm 32 project 
 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)
3. select the target to be programmed  as shown below and click on next 

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

4.select the program name 
![image](https://user-images.githubusercontent.com/36288975/226189316-09832a30-4d1a-4d4f-b8ad-2dc28f137711.png)


5. corresponding ioc file will be generated automatically 
![image](https://user-images.githubusercontent.com/36288975/226189378-3abbdee2-0df6-470f-a3cd-79c74e3d3ad8.png)

6.select the appropriate pins as gipo, in or out, USART or required options and configure 
![image](https://user-images.githubusercontent.com/36288975/226189403-f7179f1a-3eae-4637-826b-ab4ec35ba1e1.png)
![image](https://user-images.githubusercontent.com/36288975/226189425-2b2414ce-49b3-4b61-a260-c658cb2e4152.png)


7.click on cntrl+S , automaticall C program will be generated 
![image](https://user-images.githubusercontent.com/36288975/226189443-8b43451d-0b14-47e4-a20b-cc09c6ad8458.png)
![image](https://user-images.githubusercontent.com/36288975/226189450-85ffa969-2ffb-4788-81e5-72d60fdda0f1.png)
8. edit the program and as per required 
![image](https://user-images.githubusercontent.com/36288975/226189461-a573e62f-a109-4631-a250-a20925758fe0.png)

9. use project and build all 
![image](https://user-images.githubusercontent.com/36288975/226189554-3f7101ac-3f41-48fc-abc7-480bd6218dec.png)
10. once the project is bulild 
![image](https://user-images.githubusercontent.com/36288975/226189577-c61cc1eb-3990-4968-8aa6-aefffc766b70.png)

11. click on debug option 
![image](https://user-images.githubusercontent.com/36288975/226189625-37daa9a3-62e9-42b5-a5ce-2ac63345905b.png)

12. connect the  iot board to power supply and usb 

13. After connecting open the STM cube programmer 
![image](https://user-images.githubusercontent.com/36288975/227599356-9c465b7e-6bd0-436b-b4e8-742ed25e06ce.png)

14. click on UART and click on connect 
![image](https://user-images.githubusercontent.com/36288975/227599458-26976d4a-f2d4-49f0-a49f-31f46eb15761.png)

15. once it is connected , click on Erasing and programming option 
![image](https://user-images.githubusercontent.com/36288975/227599531-f03d277e-440f-4f8a-8875-97f8e8058c71.png)

16. flash the bin or hex file as shown below by switching the switch to flash mode 

![image](https://user-images.githubusercontent.com/36288975/227599656-dc4a635f-b5f1-44c8-84c5-ee0a592fa184.png)


17. check for execution of the output by switching the board to run mode 



## STM 32 CUBE PROGRAM :

```python
#include "main.h"
#include "stdio.h"
#include "stdbool.h"
bool irsensor;

void SystemClock_Config(void);
static void MX_GPIO_Init(void);
int main(void)
{
  HAL_Init();
  SystemClock_Config();
  MX_GPIO_Init();
  while (1)
  {
    irsensor=HAL_GPIO_ReadPin(GPIOA,GPIO_PIN_4);
    if(irsensor==0)
    {
    	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_0,GPIO_PIN_SET);
    	HAL_Delay(1000);
    	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_0,GPIO_PIN_RESET);
    	HAL_Delay(1000);
    }
    else
    {
    	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_0,GPIO_PIN_RESET);
    }
  }
}
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_MSI;
  RCC_OscInitStruct.MSIState = RCC_MSI_ON;
  RCC_OscInitStruct.MSICalibrationValue = RCC_MSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.MSIClockRange = RCC_MSIRANGE_6;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK3|RCC_CLOCKTYPE_HCLK
                              |RCC_CLOCKTYPE_SYSCLK|RCC_CLOCKTYPE_PCLK1
                              |RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_MSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.AHBCLK3Divider = RCC_SYSCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
}
static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
  __HAL_RCC_GPIOA_CLK_ENABLE();
  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_0, GPIO_PIN_RESET);
  GPIO_InitStruct.Pin = GPIO_PIN_0;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  GPIO_InitStruct.Pin = GPIO_PIN_4;
  GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
  GPIO_InitStruct.Pull = GPIO_PULLUP;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
}
void Error_Handler(void)
{
  __disable_irq();
  while (1)
  {
  }
}
#ifdef  USE_FULL_ASSERT
void assert_failed(uint8_t *file, uint32_t line)
{
}
#endif 
```

## Output  :
 
 ## Before detection of an object
 ![o1](1.jpg)

 ## After detection of an object
  ![o1](2.jpg)

 
 
## Result :
Interfacing a digital Input (ir pair) with ARM microcontroller based IOT development is executed and the results are verified.
