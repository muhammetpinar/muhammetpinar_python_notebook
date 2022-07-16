# manipulating text with regular expression

```python
import re #regex lib.
```

```python
text = 'this is a good day'
if re.search('good',text):
	print('wonderfull')
else:
	print('Alas :C')
#metin içerisinde good görürsen wonderfull yaz.
```

```python
text = 'Amy works diligently, Amy gets good grades. Our student Amy is succesfull.'
re.split('Amy',text)
# Amy bulur ve amyden sonrasını getirir.
```

```python
re.findall('amy',text) #text içerisinde geçtiği yerleri getir kaçtane geçti gibi.
```

```python
text = 'Amy works diligently. Amy gets good grades. Our student Amy is succesfull.'
re.search('^Amy',text)
#Amy ile başlayan cümle sayısı.
```

## patterns and character classes

```python
grades = 'ACAAAAABCCBCBAA'
re.findall('B',grades) #kaç tane B var
re.findall('[AB]',grades) #A veya B geçen kaç tane var
re.findall('[A][B-C]',grades) # A dan sonra C veya B gelenleri getir. #['AC','AB']
re.findall('AB|AC',grades) #AB veya AC olanları getir
```

```python
re.findall('[^A]',grades) #A olmayan metindekiler A dan önce başlayan gibi 
#A sonda oldugundan sorun yok
```

```python
re.findall('^[^A]',grades)   #bos dondurur cunku A ile başladıgı için bulmuyor cunku 
#a dan öncesini arıyor gibi
```

## quantifiers

```python
re.findall('A{2,10}',grades)  
#minimum 2 kere arka arkaya A geçen ve max 10 kere arka arkaya A geçenleri getir
#AAAAA  AA
```

```python
re.findall('A{1,1}A{1,1}',grades)  #tek basına olan A ları istiyoruz
#AA AA AA
```

```python
re.findall('A{2,2}',grades) #extra bosluk olmadıgı için bos dondurur
```

```python
re.findall('AA',grades)
re.findall(A{2}',grades)
#ikiside aynı dondurur
#AA AA AA 
```

```python
re.findall('A{1,10}B{1,10}C{1,10}',grades)   #azalıs trendını gorebılırız
#sonuc olarak ['AAAABC'] dondurur 
```

```python

```

```python
re.findall('[a-zA-Z]{1,100}\[edit\]',wiki)
#büyük küçük farketmez, sayısı 1 ile 100 arasında da olsun editten önceki hane sayısı
#ve sonunda edit olsun
```

```python
re.findall('[\w]{1,100}\[edit\]',wiki)   #w karakter ne olursa olsun işlevi (anywords)
#yukarıdaki ile aynı döndürür
\s herhangi bir boşluğu ifade eder
* 1 den istedigi kadar karakter sayısı olsunu ifade eder sınırlama olmadan 100 gibi
```

```python
re.findall('[\w]*\[edit\]',wiki)
#yukarıdakinin aynısını döndürür tek farkı 100 ile sınırlama olmaz
```

```python
re.findall('[\w ]*\[edit\]',wiki)#w den sonra space koyarsak önündeki 
#bosluklu ifadeleride alır
```

```python
for title in re.findall('[\w ]*\[edit\]',wiki):
	print(re.split('{\[]',title)[0])
#sadece o baslıkları dondurur
```

## groups

```python
re.findall('([\w ]*)(\[edit\])',wiki) #bütün kelimeleri gruplayarak getirir
#daha dogrusu baslıgı ayrı gruplar, editleri ayrı gruplar
```

```python
for item in re.finditer('([\w]*)(\[edit\])',wiki):
	print(item.group(1))
#sadece baslık kısımlarını getirir . her grubu indexler
```

```python
\s herhangi bir boşluğu ifade eder
* 1 den istedigi kadar karakter sayısı olsunu ifade eder sınırlama olmadan 100 gibi
a. herhangi yeni karakter 
\d herhangi rakam digit
```

```python
for item in re.finditer('(?P<tittle>[\w ]+)(?=\[edit\])',wiki):
	print(item)
#ilk grup tittle olarak adlandırıldı. herhangi bir word olur  eşleşen kayutları getirdikl 
#? ozellellikleride görmek istiyoruz. nerede oldukları gibi
```

```python

```

```python
pattern = '''
(?P<title>.*)    #universite baslıgı
(-\ located\ in\ )  #lokasyon ayırıcı
(?P<city>\w*)     #universite hangi şehirde
(,\ )       #ülke için ayırıcı
(?P<state>\w*)    #şehir hangi ülkede

'''
for item in re.finditer(pattern,wiki,re.VERBOSE):
	print(item.groupdict())

#hangi üni hangi şehir hangi ülke tuple sekilde getirir.
```

```python

```

```python

```