## Algoritma Analizi ve Tasarımı

<li> Algoritma, bir sorunun çözülmesi için tasarlanan çözüm yoludur. adımlarının açıkça belirtilmesi ve sonlu olması gerekir.
<li> Bu derste algoritmaların tasarlanması ve analiz edilmesi üzerinde durulacaktır. 
<li> Algoritmalar dersinin alındığı varsayıldığı için bazı noktalar atlanarak ya da kaynak verilerek geçilecektir. 
<li> Bazı problemlerin algoritmaları olsa da çözmek için yeterince verimli değildir. (Örneğin gerçek hayatla bire bir uyumlu bir fizik motoru yapmak için yeterli bir hesap gücü yoktur.)
<li> Bazı problemler, verimli şekilde çözülebilir. Bu derste bu çözümlerin tasarlanması ve analiziyle başlanacak ve sonra çözümü verimsiz olan problemler incelenecektir.
<br><br>

### Hesaplama Karmaşası (Computational Complexity)
<li> Algoritmanın çalışması için gerekli kaynağın (zaman ve hafıza) ölçüsüdür.

<li> Hafıza birimlerinin gittikçe ucuzlaması ve bir işin daha kısa sürede sonuç vermesi istendiğinden zaman karmaşası daha önemli kabul edilir.

<li> Küçük girdiler için algoritmalar arası büyük farklılıklar olmasa da büyük sayılarda iyi ve kötü algoritmanın süre farkı ciddi boyutlara ulaşır. Örneğin bir sayının 20 sayı arasında olup olmadığına verimli ya da verimsiz bakılması arasında problem yokken girdi sayısı 20000000 olduğu zaman verimli ve verimsiz algoritmalar arasında uçuk farklar oluşur. 
<li> Bu yüzden algoritmalarımızın analizini yaparken girdi boyutumuz n sonsuza yaklaşır şeklinde düşünürüz.

<li> Algoritma analizleri Big Oh, Big Thetha, Big Omega kullanılarak yapılabilir.
<br> 
<a href="https://www.geeksforgeeks.org/difference-between-big-oh-big-omega-and-big-theta/">Analizlerin açıklamaları için okuyabilirsiniz.</a>
<br></br>
<hr>

### Zaman Karmaşası ve Master Theorem

<li> Çeşitli problemlerin çözümünde recursive algoritmalar kullanılır. Bu algoritmaların analizleri Big Oh gibi yöntemlerle yapılamaz. 
<br></br>

<li> Recursive algoritmalar, Böl ve Fethet mantığıyla çalışır.
    <ul>
        <li> Problemleri daha küçük alt problemlere böl.
        <li> Alt problemleri çöz. 
        <li> Çözümleri birleştirerek asıl çözüme ulaş. 
    </ul>


### Master Theorem

<li> T(n) = a * T(n/b) + f(n)

<li> Master Theorem bu formülle ifade edilir. hepsini ayrı ayrı inceleyelim.
<li> T(n) bir algoritmanın çözüm süresi olsun.
<li> Eğer bu problemi a parçaya bölersek, çözmemiz gereken a tane problem olacak. input boyutumuz da 1/b katına düşsün. (Bu 1/a olmak zorunda değil. O yüzden farklı bir değişkenle ifade ediyoruz.)
<li> bir tane alt problemi çözmek, T(n/b) zaman alır. a tane problemimiz olduğu için a * T(n/b).
<li> f(n) ise problemin bölünmesi ve tekrar birleştirilmesi için geçen sürenin fonksiyonudur. Bu iki ifadenin toplamı ise bize recursive bir fonksiyonun karmaşıklık analizini verir.
<br>
<li> a, b, f(n) değerlerini bulduktan sonra sıradaki formüller uygulanır.

<ul>
    <li> Eğer f(n) < &Omicron;(n<sup>log<sub>b</sub>a</sup>) ise &Theta;(n<sup>log<sub>b</sub>a</sup>)
    <li> Eğer f(n) = &Theta;(n<sup>log<sub>b</sub>a</sup>) ise &Theta;(n<sup>log<sub>b</sub>a</sup> * log(n))
    <li> Eğer f(n) > &Omega;(n<sup>log<sub>b</sub>a</sup>) ve a * f(n/b) < c*f(n) ise &Theta;(f(n))
</ul>

<li> formüller karmaşık gelse de örnek üzerinde daha rahat açıklanabilir.
<br><br>
<div style="color: #AAA; font-size: 9pt"> Örnekler Şadi Evren Şekerin Videosundan Alınmıştır.</div>
<b> Örnek 1 </b> <br>
T(n) = 9T(n/3) + n
<br>

<li> bu örnekte, a = 9, b = 3 ve f(n) = n
<li> n <sup> log<sub>3</sub>9 </sup> = n<sup>2</sup>
<li> f(n) = n
<li> n < n<sup>2</sup> olduğu için 1. durum geçerlidir.
<li> T(n) = &Theta;(n<sup>log<sub>3</sub>9</sup>) = &Theta;(n<sup>2</sup>)
<br><br>

<!-- Merge Sort -->
<b> Örnek 2 </b> <br>
T(n) = 2T(n/2) + n
<br>
<li> bu örnekte, a = 2, b = 2 ve f(n) = n
<li> n <sup> log<sub>2</sub>2 </sup> = n<sup>1</sup>
<li> f(n) = n
<li> n = n olduğu için 2. durum geçerlidir.
<li> &Theta;(n<sup>log<sub>b</sub>a</sup> * log(n)) = &Theta;(n<sup>log<sub>2</sub>2</sup> * log(n) = &Theta;(n * log(n))
<br><br>

<b> Örnek 3 </b> <br>
T(n) = 3T(n/4) + n*log(n)
<br>

<li> bu örnekte, a = 3, b = 4 ve f(n) = n*log(n)
<li> n <sup> log<sub>4</sub>3 </sup> < n<sup>log(n)</sup>
<li> f(n) = n*log(n)
<li> n*log(n) > n <sup> log<sub>4</sub>3 </sup> olduğu için 3. duruma uygundur.
<li> üçüncü durum için bir şartı daha kontrol etmemiz gerekir.
<li> a * f(n/b) < c * f(n) olacak şekilde 1'den küçük bir c olmalıdır. 
    <ul>
        <li> eşitsizlikteki ifadeleri yerine yazıp düzenleyelim.
        <li> 3 * f(n/4) < c * f(n)
        <li> 3 * n/4 * log(n/4) < c * n * log(n)
        <li> 3/4 * n * log(n/4) < c * n * log(n)
    </ul>
<li> ifadenin düzenlenmiş halinde c yerine eşitsizliği sağlayacak 1'den küçük bir sabit koyabiliriz. Bu sebeple 3. kural geçerlidir.
<li> T(n) = &Theta;(f(n)) = &Theta;(n * log(n))
<hr>

### Ek
<li> <a href="https://www.geeksforgeeks.org/difference-between-big-oh-big-omega-and-big-theta/">Big O, Big Omega ve Big Theta Farkları</a>
<li> <a href = "https://www.youtube.com/watch?v=yfIbsFfOTt8"> Şadi Evren Şeker Master Theorem 
