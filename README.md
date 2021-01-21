# CDF nedir?
Olasılık kuramı ve istatistik bilim dallarında birikimli dağılım fonksiyonu bir reel değerli rassal değişken olan Xin olasılık dağılımını tümüyle tanımlayan bir fonksiyondur. Olasılık dağılım fonksiyonu veya sadece dağılım fonksiyonu olarak da anılmaktadır. Her bir reel sayı olan x için X'in birikimli dağılım fonksiyonu şöyle ifade edilir:
x -> FX(x)=P(X<=x),
Burada sağ taraf xe eşit veya xden daha küçük değerler alan rassal değişken X için olasılık değerlerini temsil eder. Böylece, Xin (a, b] aralığında bulunma olasılığı

FX(b)-FX(a) if() a < b. olur.

Matematik notasyon kullanma kuralı şöyle uygulanır: Eğer birkaç rassal değişken X, Y, ...vb. kullanılırsa alt-endeksler verilir ama tek rassal değişken kullanılırsa alt-endeks verilmez. Bir başka notasyon kullanış kuralına göre, birikimli dağılım fonksiyonu F için, olasılık yoğunluk fonksiyonu veya olasılık kütle fonksiyonu için f kullanılmalıdır. Bu notasyon kullanılma kuralları genellikle olasılık konuları için geçerlidir; ancak bazı özel olasılık dağılımları (örneğin normal dağılım) için sırf o fonksiyonlar için özel notasyon kullanılır.

X için birikimli dağılım fonksiyonu, olasılık yoğunluk fonksiyonu olan f terimi ile şöyle ifade edilir:

F(x)=∫F(t)dt (-∞ to x)

Dikkat edilmelidir ki verilen tanımlama içinde bulunan '≤' (eşit ve daha az) işareti bir klasik kullanılma alışkanlığından ortaya çıkmıştır ve diğer bir şekilde '>=' olma imkânı da vardır. '≤' genellikle kullanıldığı için bu konvensiyona uyulacaktır. Binom ve Poisson dağılımları için hazırlanmış ve pratik problem çözümleri için genellikle kullanılan olasılık tabloları da bu tür tanım kullanırlar. Karakteristik fonksiyon için Levy'nin ters bulma formülü gibi önemli formüller de bu (eşit ve daha az) kullanımına dayandırılmıştır.

Normal dağılım, aynı zamanda Gauss dağılımı veya Gauss tipi dağılım olarak isimlendirilen, birçok alanda pratik uygulaması olan, çok önemli bir sürekli olasılık dağılım ailesidir.

Bu dağılım ailesinin her bir üyesi sadece iki parametreyle tam olarak tanımlanabilir: Bunlar konum gösteren ortalama (μ, aritmetik ortalama) ve ölçek gösteren varyans (σ2, "yayılım")dır.

Olasılık kuramı içinde birkaç sürekli olasılık dağılımları ve ayrık olasılık dağılımlarının limite giden dağılımları yani rassal değişkenlerin yakınsama analizinde kullanılmaktadır.

--Görüntü analizinde CDF--

Eşikleme: Görüntü işlemede en çok kullanılacak tekniklerden biri eşiklemedir (treshold). Gri ton eşiklemesinde bir eşik değer seçilerek, açık ton üzerinde koyu kısımların yada tersi olarak koyu zemin üstünde parlak kısımların aranması hedeflenir. Bunun sonucunda “obje” ve “arka plan” olarak iki kısım belirlenir. Eşik değerin belirlenmesi için görüntünün parlaklık histogramı çıkartılır. Yüksek değere sahip olan kısımlar daha açık renkteki kısımları, yani bu görüntü  için arkaplanı göstermekte, daha düşük değerde olan
kısımlar ise objeleri göstermektedir. Renkli görüntülerde ise bir piksel temelde üç renk bileşeni içerir (RGB: kırmızı,yeşil, mavi). Bu bileşenlerin her biri bir byte ile anlatıldığında her bir piksel 255*255*255 farklı renk değeri alabilir. Bir pikselin ikili uzaya aktarılması onun renk bileşenlerinin tümünün 255 ya da tümünün 0 olması anlamına gelir. Bunun için de piksel renk bileşeni bir sınırdan büyükse 255 küçükse 0 yapılır. RGB renk uzayı ışığı temel alarak, doğadaki tüm renklerin kodları bu üç temel renge referansla belirtilir. HSV (Hue, Saturation, Value) veya HSB (Hue,Saturation, Brightness) renk uzayında ise renkleri sırasıyla renk özü, doygunluk ve parlaklık olarak tanımlar. Renk özü, rengin baskın dalga uzunluğunu belirler, örneğin sarı, mavi, yeşil, vb. Açısal bir değerdir (0°-360°). Doygunluk ise rengin canlılığını belirler. Yüksek doygunluk canlı renklere neden olurken, düşük olasılık rengin gri tonlarına yaklaşmasına neden olur ve 0-100 arasında değişir. Parlaklık ise rengin aydınlığını yani içindeki beyaz oranını belirler. 0-100 arasında değişir. RGB ve HSV nin bileşenlerinin histogramları üzerinde seçim yapılarak eşikleme gerçekleştirilir.

Aşağıda belirtilen pyhton kodlama ile yukarıdaki görüntü işleme tekniği örneklemesi yapılmıştır.


import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import numpy as np
import pandas as pd

from skimage.io import imshow, imread
from skimage.color import rgb2gray
from skimage import img_as_ubyte, img_as_float
from skimage.exposure import histogram, cumulative_distribution

* resmimizi ekliyoruz ve matrisini gösteriyoruz
img = mpimg.imread('C:fotograf yolu')
print(img)
imgplot = plt.imshow(img)
plt.show()

* resmi gri tona döndürüyoruz
plt.figure(num=None, figsize=(8, 6), dpi=80)
dark_image_grey = img_as_ubyte(rgb2gray(img))
plt.imshow(dark_image_grey)
plt.show()

# histogramını çıkarma işlemi
freq, bins = histogram(dark_image_grey)
plt.figure(num=None, figsize=(8, 6), dpi=100, facecolor='white')
freq, bins = histogram(dark_image_grey)
plt.step(bins, freq / freq.sum())
plt.xlabel('intensity value', fontsize=12)
plt.ylabel('fraction of pixels', fontsize=12)
plt.show()

# histogram normal dağılıma sahip değil. Teorik olarak CDF düz bir çizgide olmalıdır amacımız
# bu resmi normal dağılım yapabilmek.


freq, bins = cumulative_distribution(dark_image_grey)
target_bins = np.arange(255)
target_freq = np.linspace(0, 1, len(target_bins))
interpolation = np.interp(freq, target_freq, target_bins)
dark_image_eq = img_as_ubyte(interpolation[dark_image_grey].astype(int))
freq_adj, bins_adj = cumulative_distribution(dark_image_eq)

fig, axes = plt.subplots(1, 2, figsize=(15, 7));
imshow(dark_image_grey, ax=axes[0])
imshow(dark_image_eq, ax=axes[1])


axes[0].axis('off')
axes[1].axis('off')
axes[0].set_title('Unadjusted Image', fontsize=17)
axes[1].set_title('Adjusted Image', fontsize=17)

fig, axes = plt.subplots(1, 1, figsize=(19, 7));
plt.step(bins, freq, c='blue', label='Actual CDF')
plt.step(bins_adj, freq_adj, c='purple', label='Adjusted CDF')
plt.plot(target_bins,
         target_freq,
         c='red',
         label='Target CDF',
         linestyle='--')

plt.legend(prop={'size': 14})
plt.xlim(0, 255)
plt.ylim(0, 1)
plt.xlabel('Intensity values', fontsize=15)
plt.ylabel('Cumulative fraction of pixels', fontsize=15)
plt.show()


plt.step(bins, freq / freq.sum())
plt.xlabel('intensity value', fontsize=12)
plt.ylabel('fraction of pixels', fontsize=12)
plt.show()
imshow(dark_image_eq);
plt.show()

freq_adj, bins_adj = cumulative_distribution(dark_image_eq)






















