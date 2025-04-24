
# PWM LED Dimmer - STM32

Bu proje, STM32F4 serisi bir mikrodenetleyici kullanılarak PWM (Pulse Width Modulation) tekniğiyle bir LED'in parlaklığını yazılım üzerinden artırıp azaltmayı amaçlar.

## Donanım Gereksinimleri
- STM32F4 geliştirme kartı 
- LED 
- 330Ω direnç 
- Breadboard ve jumper kablolar 

## Bağlantı Şeması
```
PA6 (TIM3_CH1) ----> 330Ω ----> LED ----> GND
```


## Açıklamalar 
Timer, PWM modunda yapılandırılmıştır. LED'in parlaklığı CCR değeri değiştirilerek kontrol edilir. Kod içinde `__HAL_TIM_SET_COMPARE()` fonksiyonu ile duty cycle yazılımsal olarak artırılıp azaltılır. Böylece LED'in parlaklığı yavaşça artıp azalır.

### 1. Hesaplamalar

![HESAPLAMALAR](https://github.com/user-attachments/assets/59360c74-cf56-4f48-94ce-92b41c5928c6)

- ARR = 999
- CCR = 250 → Duty Cycle = (999/250) = ~%25 duty cycle (düşük parlak) [0.25 ms HIGH, 0.75 ms LOW]
- CCR = 500 → Duty Cycle = (999/500) = ~%50 duty cycle (yarı parlak) [0.5 ms HIGH, 0.5 ms LOW]
- CCR = 999 → %100 duty cycle (tam parlak) [1 ms HIGH]

Aslında projede belirtilen LED parlaklığnı ayarlamak sadece LED'in HIGH olma süresini oynamaktan ibaret. 

### 2. Kod 
```
uint32_t pwm_value = 0;
uint8_t direction = 1;

int main(void)
{
  HAL_TIM_PWM_Start(&htim3, TIM_CHANNEL_1);   
  
  while (1)
  {
      __HAL_TIM_SET_COMPARE(&htim3, TIM_CHANNEL_1, pwm_value);
  
      HAL_Delay(10);  // Geçişin yavaş olması için bekleme
  
      if (direction)
      {
          pwm_value += 10;
          if (pwm_value >= 999)
              direction = 0;
      }
      else
      {
          if (pwm_value > 10)
              pwm_value -= 10;
          else
              direction = 1;
      }
  }
}
```
1. Belirtilen parametrelere(Prescaler, ARR) göre Timer 3'ün 1. kanalından PWM sinyali üretilmeye başlar.
```c
 HAL_TIM_PWM_Start(&htim3, TIM_CHANNEL_1);
```

2. PWM sinyalinin duty_cycle oranını(CCR) kontrol etmek için değişkenler tanımlanır.

```c
uint32_t pwm_value = 0;     // CCR değeri: 0 → 999(ARR) arasında
uint8_t direction = 1;      // 1: artan parlaklık, 0: azalan
```

3. PWM için her şey hazır! (ARR, CCR, Duty_Cycle)
```c
while (1)
{
  __HAL_TIM_SET_COMPARE(&htim3, TIM_CHANNEL_1, pwm_value);
  HAL_Delay(10);

/* Eğer direction = 1 ise, PWM değeri 10'ar 10'ar artar → LED yavaşça parlar. */
  if (direction)      
  {
    pwm_value += 10;
    if (pwm_value >= 999) direction = 0;    // pwm_value 999’a ulaşınca (Duty Cycle %100) → direction = 0 yapılır → artık azalmaya başlar.
  }
  else
  {
    if (pwm_value > 10) pwm_value -= 10;
    else direction = 1;
  }

// Bu şekilde LED sonsuz döngüde parlaklık artar → azalır → artar...
```

## Proje Videosu 


https://github.com/user-attachments/assets/145cfed8-c3f9-4dc9-8433-f40f2f0fb4b5

