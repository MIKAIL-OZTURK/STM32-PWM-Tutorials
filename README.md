# 1. PWM Nedir ? 

**PWM**, dijital bir sinyali belirli frekansta aç-kapa yaparak ortalama gerilim seviyesini kontrol etmeye yarayan bir tekniktir. Analog sinyal üretmeye alternatif bir yöntemdir.



### Temel Parametreler
- **Duty Cycle**: Sinyalin 1 (HIGH) olduğu sürenin, toplam periyoda oranıdır
- **ARR (Auto-Reload Register)**: PWM sinyalinin toplam süresidir (periyot)
- **CCR (Capture/Compare Regiser)**: PWM sinyalinin 1 (HIGH) olduğu süredir


                               
```
Duty Cycle (%) = (CCR / ARR) * 100
```


# 2. PWM Nasıl Üretilir ?
PWM sinyali, Timer modulleriyle oluşturulur. 

1. PWM sinyalinin toplam süresi belirlenir --> ARR Register
2. PWM sinyalinin HIGH süresi belirlenir --> CCR Register



![image](https://github.com/user-attachments/assets/1b9de78a-5bad-477a-b9ac-3b61fecfaa01)

```
  CNT < CCR     -> HIGH
  CNT >= CCR    -> LOW
```
  




