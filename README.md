# 1. PWM Nedir ? 

**PWM**, sabit frekansta ama değişken görev çevrimli (duty cycle) bir kare dalga üretme yöntemidir. Bu yöntem sayesinde dijital pinlerle analog benzeri davranışlar elde edilir.


# 2. PWM Teknik Detayları

### a. Temel Terimler
- **Frequency (Frekans)**: PWM sinyalinin saniyedeki periyot sayısıdır (Hz)

- **Duty Cycle (%)**: HIGH seviyede geçirilen sürenin toplam periyoda oranıdır

- **Resolution (Çözünürlük)**: PWM sinyalinin adımlama hassasiyeti. Bit cinsinden ifade edilir (örneğin: 8-bit PWM → 256 farklı duty cycle değeri)


# 3. PWM Nasıl Üretilir ? (STM32)

### a. Temel Terimler
- **Prescaler**: Sistemin clock frenkansını böler
- **Auto-Reload Register (ARR**): PWM periyodunu belirler
- **Capture/Compare Register (CCR)**: Duty cycle'ı belirler


### b. Temel Formüller 

- **Duty Cycle**                                   
```
Duty Cycle (%) = (CCR / ARR) * 100
```


- **PWM Frekansı**

```
PWM Frequency = Timer_Clock / ((PSC + 1) * (ARR + 1))
```





