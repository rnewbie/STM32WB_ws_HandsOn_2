# HandsOn_2

Created on: Sep 22, 2021

Author: realmer

This is completed lab 2 from STMicroelectronics [STM32WB workshop](https://www.st.com/content/st_com/en/support/learning/stm32-education/stm32-moocs/STM32WB_workshop_MOOC.html)

Workshop materials are quite outdated, this solution was done with stm32wb cube package version 1.12.1 and STM32CubeIDE version 1.7.0 with the help of video 4 from [BLE security with STM32WB training](https://www.st.com/content/st_com/en/support/learning/stm32-education/stm32-moocs/bluetooth-low-energy-security-with-stm32wb-mooc.html)
     
Diffferences from original workshop:

- You don't need to deal with IPCC and RTC interrupts. It's done in BLE wizard automagically
- You don't need to deal with HSE tuning. Same as previous.
- You don't need to add scheduler (sequencer now) call in a main loop. Pay attention, all calls changed from SCH_xx to UTIL_SEQ_xxx 
- You have to add sequencer id (CFG_TASK_SW1_BUTTON_PUSHED_ID) for P2PS_Send_Notification manually in Core/Inc/app_conf.h to CFG_Task_Id_With_HCI_Cmd_t    
- to make EXTI interrupt work you should unmask it for LP wakeup in Core/Src/app_entry.c -> MX_APPE_Init
```
/* USER CODE BEGIN APPE_Init_1 */
APPD_Init();
LL_EXTI_EnableIT_0_31(LL_EXTI_LINE_0 | LL_EXTI_LINE_1 | LL_EXTI_LINE_4);
/* USER CODE END APPE_Init_1 */
```
- usart DEBUG messaging is enabled on USART1, connected to st-link with baud 230400 8N1.
     