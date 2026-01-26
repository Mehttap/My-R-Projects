# Tgss datasetinde türkiye'deki araç sahipliğinin dağılım grafiği
```
tgss <- read_sav("~/Desktop/Veri Analizi Ders Notları R/TGSS  2024.sav")
tgss1=look_for(tgss)

ggplot(tgss)+
  geom_bar(aes(x=as_factor(houcar)))+
  labs(x="Araç Sahipliği",
       y="Sayı")+
  annotate("text", x=2, y=1450, label="Araç Sahibi")+
  theme()+
  theme_bw()
```
# Araç sahibi sayısının kentleşme alt gruplarına göre dağılım grafiği 
### (kırsal,orta yogun kent, yogun kent) 
##### (facet_wrap)
```
ggplot(tgss)+
  geom_bar(aes(x=as_factor(houcar)))+
  labs(x="Araç Sahipliği",
       y= "Sayı")+
  facet_wrap(~degurba)+
  theme()+
  theme_bw()
```

# Sub(alt)grupların etiketlerini grafiğe ekleme 
### (degurba değişkenini kategorik yap)
```
ggplot(tgss)+
  geom_bar(aes(x=as_factor(houcar)))+
  labs(x="Araç Sahipliği",
       y= "Sayı")+
  facet_wrap(~ as_factor(degurba))+
  theme()+
  theme_bw()
```
# Grafikteki sütunlara renk ve çerçeve ekleme
```
ggplot(tgss,aes(x=as_factor(houcar) ))+
  geom_bar(fill="pink", colour="grey")+
  labs(x="Araç Sahipliği",
       y= "Sayı")+
  facet_wrap(~ as_factor(degurba))+
  theme()+
  theme_bw()
```
# Grafikte çıkan NA değerleri silme
```
tgss %>%
  filter(!is.na(houcar))%>%
ggplot(aes(x=as_factor(houcar) ))+
  geom_bar(fill="pink", colour="grey")+
  labs(x="Araç Sahipliği",
       y= "Sayı")+
  facet_wrap(~ as_factor(degurba))+
  theme()+
  theme_bw()  
```

# Bir değişkenin içerisindeki değerlere bakma 
### (eğitim değişkeninde neler var bakalım)

```
attributes(tgss$educ)

```

# Datasetindeki mevcut değişkenleri yeniden gruplama/kodlama 

(MYO,4-5-6 yıllık Fakülte ve 4 yıllık fakülte hepsini üni mezunu yap) (recode yapma işlemi)

### 1.Yol-Uzun Versiyon
```
tgss %>% mutate(educ6= case_when(
  educ== 1 ~ 1,
  educ== 2 ~ 2,
  educ== 3 ~ 3,
  educ== 4 ~ 4,
  educ== 5 ~ 5,
  educ== 6 ~ 5,
  educ== 7 ~ 6,
  educ== 8 ~ 6,
))

```
