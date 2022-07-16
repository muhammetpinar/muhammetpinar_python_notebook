# Python Definitions

```python
def merhaba():
	print("MERHABA DUNYA")
merhaba()
```

### faktoriyel hesaplayan definition

```python
def faktoriyel(sayi):
    faktoriyel = 1 
    for i in range(1,sayi+1):
        faktoriyel = i*faktoriyel
    print(faktoriyel)

faktoriyel(4)
```

### return kullanırsam print’e gerek kalmaz

```python
def faktoriyel(sayi):
    faktoriyel = 1 
    for i in range(1,sayi+1):
        faktoriyel = i*faktoriyel
    return faktoriyel

faktoriyel(4)
```

### varsayılan değer alınan fonksiyonlar

ekrana ad ve soyadı yazacaktır. TC KİMLİK VE YAS BİLGİ YOK OLARAK DONECEKTIR.

```python
def giris_ekrani(AD = 'BILGI YOK', SOYAD = 'BILGI_YOK',TCKIMLIK_NO= 'BILGI_YOK',YAS =  'BILGI_YOK'):
    print("Kullanıcı bilgileri yükleniyor...")
    print("AD = {}\n SOYAD = {}\n TCKIMLIK_NO = {}\n YAS ={}\n".format(AD,SOYAD,TCKIMLIK_NO,YAS))
bilgiler = giris_ekrani(AD = 'MUHAMMET',SOYAD = 'PINAR')
bilgiler
```

### YEREL VE GLOBAL DEGİSKENLER

içerideki a yerel degiskendir sadece tanim fonksiyonuna özeldir dışarda a diye çağrılamaz.

```python
def tanim():
	a = 5
	print(a)
tanim()
```

a global değişkendir nerede çağırırsam orada çalışır

```python
a = 5
print(a)
```

global a değişkeni içerdeki ifadeyi sabitleyerek dışarı 10 olan a’yıda 2 yaparak çıkarır.

```python
a  = 10 
def printing():
    global a
    a = 2 
    print(a)
printing()
print(a)
```