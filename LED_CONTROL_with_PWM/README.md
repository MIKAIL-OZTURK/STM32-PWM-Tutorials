
# PWM LED Dimmer - STM32

Bu proje, STM32F4 serisi bir mikrodenetleyici kullanılarak PWM (Pulse Width Modulation) tekniğiyle bir LED'in parlaklığını yazılım üzerinden artırıp azaltmayı amaçlar.

## Donanım Gereksinimleri
- STM32F4 geliştirme kartı (ör. STM32F401RE, STM32F407VG)
- LED (veya kart üzerindeki dahili LED)
- 330Ω direnç (harici LED için)
- Breadboard ve jumper kablolar (isteğe bağlı)

## Bağlantı Şeması
```
PA6 (TIM3_CH1) ----> 330Ω ----> LED ----> GND
```

## CubeMX Ayarları
- **TIM3** → Channel 1 → PWM Generation CH1
- **Prescaler**: 83 (84 MHz / 84 = 1 MHz)
- **ARR (Auto Reload)**: 999 → PWM frekansı: 1 kHz (periyot = 1 ms)
- **GPIO PA6** → Alternate Function → TIM3_CH1

## Açıklama ve Hesaplamalar
Timer, PWM modunda yapılandırılmıştır. LED'in parlaklığı CCR değeri değiştirilerek kontrol edilir. Kod içinde `__HAL_TIM_SET_COMPARE()` fonksiyonu ile duty cycle yazılımsal olarak artırılıp azaltılır. Böylece LED'in parlaklığı yavaşça artıp azalır.

![HESAPLAMALAR](https://github.com/user-attachments/assets/59360c74-cf56-4f48-94ce-92b41c5928c6)

- ARR = 999
- CCR = 500 → %50 duty cycle (yarı parlak)
- CCR = 250 → %25 duty cycle (düşük parlak)
- CCR = 999 → %100 duty cycle (tam parlak)

  
## Proje Videosu 


https://github.com/user-attachments/assets/145cfed8-c3f9-4dc9-8433-f40f2f0fb4b5

