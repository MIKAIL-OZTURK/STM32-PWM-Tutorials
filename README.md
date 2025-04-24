# 1. PWM Nedir ? 

**PWM**, bir dijital sinyali aç/kapa (1/0) şeklinde belirli bir frekansta ama farklı sürelerde açık kalacak şekilde üretmektir. Belirli bir süre boyunca sinyal “1” (HIGH) olur, sonra “0” (LOW) olur. Bu döngü sürekli tekrar eder ama esas 
olay şu: “1” olma süresini değiştirerek bu sinyalin ortalama gücünü kontrol edersin.


### PWM'nin En Önemli Parametresi: Duty Cycle
**Duty Cycle**: Sinyalin 1 (HIGH) olduğu sürenin, toplam periyoda oranı

%100 → Sinyal hep HIGH (kesintisiz güç)

%0 → Sinyal hep LOW (hiç güç yok)

%50 → Yarım zaman açık, yarım zaman kapalı

```
%25 Duty: [___---___---___---]  (az açık)
%50 Duty: [___===___===___===]  (yarı açık)
%75 Duty: [___###___###___###]  (çok açık)

```


# 2. STM32 Timer ile PWM Nasıl Üretilir?
1. Timer bir periyot süresi belirler (ARR register)

2. Sen bu periyodun ne kadarında çıkışı “1” yapmak istiyorsan, onu CCR register’a yazarsın

3. Timer her periyot başında sıfırlanır ve tekrar sayar

4. Sayı CCR'a gelince çıkış LOW olur → PWM oluşur


### b. Temel Formüller 

- **Duty Cycle**                                   
```
Duty Cycle (%) = (CCR / ARR) * 100
```


- **PWM Frekansı**

```
PWM Frequency = Timer_Clock / ((PSC + 1) * (ARR + 1))
```





