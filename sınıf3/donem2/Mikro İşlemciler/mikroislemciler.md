Hürmetler. Hataları bildirmek için destekleme isteği(PR) atabilir veya e-posta yoluyla <a href="mailto:alpkut55@gmail.com">ulaşabilirsiniz</a>.<br/>
Şimdi konumuza gelelim okulumuz(Gazi Evrenkenti Mühendislik Bölümcesi) Elektrik-Elektronik Mühendisliği öğrencileri bu derste ARM Assembly görecekleri için bu kaynak onlar adına çok faydalı olmayacağı kanısındayım.
Bu derste öncelikle Assembly ve doğası hakkında konuşmak isterim. Assembly her aletin(işlemcinin) yapısına:
- Komut Seti Yapısına (ISA)
- İşlemci Mimari Yapısına<br/>
bağlıdır. Yukarı seviyeden(high level) bakınca çok ilkel gelebilir ama bilgisayar biliminin transistörün icadından sonraki çağına baktığımızda çok *manyak* bir şey olduğunu anlıyoruz.<br>

Her "mikroişlemci ve assembly" kitabında iki haneli sayıda giriş kısmı bulunur, bu kısmın hikayesini
<details><summary>buraya tıklayarak açıp okuyabilirsiniz</summary>
<p> 
Bu gelişimi şöyle özetleyim: bilgisayar bilimi transistörün icadından sonra sayısal tasarım harikaları olduğu kavranmış lâkin ortada bir birlik olmadığını görmüşler. Her bilgisayar kendi başına bir cumhuriyet olduğu dönemlerde insanlık kendisi gibi kavga dövüşsüz birlik olunca daha güçlü olduğunu bildiği gibi bilgisayar biliminin de daha güçlü olabileceğini kavramışlar ve bir ortak zemin kurmak istemişler sonuçta kim yanında hayvan gibi delikli programlama kayıtçısı taşımak ister ki?<br>
<div style="margin-left:auto,margin-right: auto" align="center"><img src="https://i.ytimg.com/vi/wALFrUd6Ttw/hqdefault.jpg" alt="punch card and altair 8800"><br/>soldan akıp giden gri şerit delikli programlama kayıtçısı(punched card)<img/></div><br/>

Sonrasında çeşitli diller geliştirilmiş ki insanlar farklı bilgisayarlar kullansa da ortak bir yazılım tabanında yazılım geliştirilebilsin. Bu arada yazılım demişken epeydir bir zaman tartışma konusu olan "kadın yazılımcılar", "abi erkekler her işte olduğu gibi yazılımda da kadınlardan üstün" tarzı aptalca hikayeler gezmekte lâkin gerçeği biliyor musunuz?<br/>

<div style="margin-left:auto,margin-right: auto" align="center"><img width="300" src="https://media1.tenor.com/images/0d0077a13fff517c97916da3ccb27ec8/tenor.gif?itemid=17051074"/></div></br>

_İlk yazılımcılar arasında erkek yok denecek kadar azdır bunun  asıl nedeni gâvurların 70li yıllara kadar yazılımın değerini kavrayamaması ve asıl işin donanımda olduğunu düşünmesinden dolayı yazılım için "software" yani "cıvık-yumuşak mal" muamelesi yapmaları bu yüzden erkeklere yakıştırılmamasıdır; "hardware" ise "sert-zor mal" anlamına gelip bu iş için daha fazla nitelik gerektirdiğini düşünmeleridir._</br>

Giriş kısmını geride bıraktığımıza göre Assembly nedir kısmına hafiften gelelim.
</p>
</details>

# Assembly Nedir?
Assembly makina dili üzerinde bulunan ve kendi makina-kod dönüştürücüsü(assembler) yardımıyla yazılan kodu makina diline çeviren bir güzelliktir. C yazdığınızda C derleyicisi kodu Assembly'ye onu da makina koduna çevirir. Bu çevirimde arada olan güzellikleri listelersek listemiz şu şekilde olacaktır.
- derleyici(compiler)
- bağlayıcı(linker) 
- makina-kod dönüştürücüsü(assembler)<br/>
Bu ders kapsamında bu üç elemana gerek duymayacağız ve bir Intel 8086 işlemcisi ![öykünücüsü(emülatörü)](https://medium.com/@ozkancakirwork/em%C3%BClat%C3%B6r-nedir-nas%C4%B1l-kullan%C4%B1l%C4%B1r-bbf8a0b5d19a) ile öğreneceğiz x86 Assembly'i.

# Emu8086
Yazacağımız x86 Assembly kodlarımızı üzerinde öykünetebileceğimiz(emule) bir öykünücüdür. Kullanımı ve genel olarak burayla ilgili açıklamalar için ![bu linke](https://roboturka.com/pic-assembly-pic-c/assembly-ve-emu8086/) bakabilirsiniz.</br>
Ve ![bu bağlantı](https://emu8086-microprocessor-emulator.en.softonic.com/)dan indirilebilir.

# Assembly İlk Adımlar
Komutlar basittir ve programın "help" düğmesinden rahatça erişilebilmektedir.
![image](https://user-images.githubusercontent.com/44534126/113336434-16312e80-932f-11eb-96c6-66de733c2bb8.png)
Burada yukarıdan "8086 Instruction Set" bağıntısına tıklayarak tüm komutların listesine ulaşabilirsiniz.
Yüksek ihtimal tüm komutlara ihtiyacınız olmayacak olursa da buradan okuyabilirsiniz.
Burada şunu belirtmek gerekir ki bu kaynağın oluşturulma amacı bir şeyi öğretmek değil, bir şeyi nasıl öğrenilebileceğini öğretmek; bu sebeble komutların aldığı işleçleri, nasıl kullanıldıklarını veya ne işe yaradıklarını yazmayacağım.
Kesinlikle bilinmesi gerekenler:
- ADD
- AND
- CALL
- CMP
- DIV
- INT
- J[bayrakları ilgirendiren durumlar] : JC, JNB, JG, Jl
- JMP
- LEA
- LOOP
- MUL
- MOV
- NOT
- OR
- POP
- PUSH
- SUB
<br/>Liste, üzerine düzgünce düşünülürse uzayıp gidebilir lâkin gerek görmedim. Bunların durumsal hallerini, çeşitli bayraklar ile etkileşimde olduğu zamanki hallerini yardım dökümanından kendi başımıza karıştırıp, kod örnekleri inceleyip öğreniminizi verimli hale getirebilirsiniz.

## İyi bu komutları öğrenelim de reg ne memory ne immediate ne sreg ne?
Tüm komutlar olmasa da çoğu komutlar "operand" denilen işleçlerle çalışır ve bunların dökümantasyondan layığıyla öğrenilmesi gerekli yoksa ekrana, _uygun tabirle_, mal gibi baktırır. 

### REG(register/yazmaç) 
Var olanlar: AX, BX, CX, DX, AH, AL, BL, BH, CH, CL, DH, DL, DI, SI, BP, SP.
Burada ikinci karakteri X'li olan yazmaçlar 16 bit yazmaçlardır. 2. karakterdeki L=low(düşük) ve H=High(üst) 8'li bit dizilerini ifade eder; P=Pointer(işaretçi) bir şeyi işaret eden yazmaçlarda görürüz.

![image](https://user-images.githubusercontent.com/44534126/113339744-9e193780-9333-11eb-9d17-dbb3fd69ee22.png)

### Memory(hafıza)
Adı üstünde hafızadaki konumu niteler. Köşeli parantezler içinde  BX, SI, DI, BP yazmaçları ile kullanılabilir, burjuvalar gibi [segment:konum] şeklinde kulllanmaya çalışmayın.  

### Immediate(Hazır değer)
Çeşitli tabanlardaki, _ikilik, sekizlik, onluk, onaltılık_, sayıların şap diye işleç olarak kullanılan halidir.
Örnek:
```assembly
mov al, 123 ;buradaki al yazmacına(alanı 2^8= 1byte= ondalık tabanda sınırlar dahil 0-256) ondalık tabanda şap diye 123 değerini girdik.
;bir zımbırtı belirlemezsek hazır değerlerimiz ondalık olarak işlem görür
;123h deseydik onaltılık tabanda işlem görecekti
;123b diyemezdik çünkü 2lik tabanda yalnızca 0 ve 1 var :D
;123o deseydik sekizlik tabanda işlem görecekti
```
### SREG(segment yazmacı)
Buradaki yazmaçlar segment ifade eder.
![image](https://user-images.githubusercontent.com/44534126/113344836-48945900-933a-11eb-83a7-e5874600bcc6.png)


# Kod Örnekleri
Kod okunmadan öğrenilemeyeceği için ihtiyaç duyabileceğiniz çeşitli kodları buraya bırakıyorum.

### dizideki en küçük sayıyı bulma
<details><summary>ilgili kodu görmek için tıklayınız</summary>
<p> 
          
```assembly 
org 100h
lea bx, data        ; datanin bellege yerlestirilmeye baslandigi adres
mov si, 0           ; incelecek indisi tutan zımbırtı
mov cx, 5           ; loop kontrolu için cx'e değer ataması gerekmektedir
mov al, [bx]        ; dizimizin ilk elemanını al'ye atıyoruz
;         burada al kullanılması sebebi sayıların 256dan küçük olması ve 256dan küçük olduğunda
;         birden fazla mov komutu ile ax'e atama yaparsak önce al'ye sonra sonra ah'ye atacak sonra işler karışacaktır. 
;         arada böyle olur çok takmayın.
enkucukbul:
    mov dl, [bx+si] ; ilk eleman al'de tutuluyor, dl'de sonraki elemana bakılacak.
    cmp al, dl      ; bir sonraki eleman daha mı küçük? (1)
    jg kucukdegistir; bir sonraki eleman daha küçükse kucukdegistir'e atla (2)
    inc si          ; kaynak indisi(source index) arttır
    loop enkucukbul ; cx=cx-1, jmp enkucukbul
    jmp bulundu     ; bulundu'ya atla, eğer bunu yazmasaydık döngü bittiğinde alttan satır satır işlemeye devam ederdi.
kucukdegistir: 
    mov al, 0       ; biz ayağımızı denk alalım
    mov al, dl      ; dl daha küçüktü ya ondan onu al'ye alıyoruz çünkü küçük sayıyı al'de tutmamız gerek (1)'deki ve (2)'deki mantıktan ötürü
    inc si          ; si artacak uleyn
    loop enkucukbul ; cx=cx-1, jmp enkucukbul
bulundu:
    ret
data db 12, 20, 10, 14, 5
    end       
```
</p>
</details>          
          
          
          
### dizideki en büyük sayıyı
<details><summary>ilgili kodu görmek için tıklayınız</summary><p>

```assembly
org 100h
lea bx, data        ; datanin bellege yerlestirilmeye baslandigi adres
mov si, 0           ; incelecek indisi tutan zımbırtı
mov cx, 5           ; loop kontrolu için cx'e değer ataması gerekmektedir
mov al, [bx]        ; dizimizin ilk elemanını al'ye atıyoruz
;         burada al kullanılması sebebi sayıların 256dan küçük olması ve 256dan küçük olduğunda
;         birden fazla mov komutu ile ax'e atama yaparsak önce al'ye sonra sonra ah'ye atacak sonra işler karışacaktır.
;         arada böyle olur çok takmayın.
enbuyukbul:
mov dl, [bx+si] ; ilk eleman al'de tutuluyor, dl'de sonraki elemana bakılacak.
cmp al, dl      ; bir sonraki eleman daha mı büyük? (1)
jl buyukdegistir; bir sonraki eleman daha büyükse büyükdegistir'e atla (2)
inc si          ; kaynak indisi(source index) arttır
loop enbuyukbul ; cx=cx-1, jmp enbuyukbul
jmp bulundu     ; bulundu'ya atla, eğer bunu yazmasaydık döngü bittiğinde alttan satır satır işlemeye devam ederdi.
buyukdegistir:
mov al, 0       ; biz ayağımızı denk alalım
mov al, dl      ; dl daha büyüktü ya ondan onu al'ye alıyoruz çünkü büyük sayıyı al'de tutmamız gerek (1)'deki ve (2)'deki mantıktan ötürü
inc si          ; si artacak uleyn
loop enbuyukbul ; cx=cx-1, jmp enbuyukbul
bulundu:
ret
data db 12, 20, 10, 14, 5
end
```
</p></details>

### kabarcık sıralama
<details><summary>Kabarcık sıralama kodunu görmek için tıklayınız</summary>
<p>
Buyrunuz

```assembly
org 100h ; programı başlatmak için
lea bx, dizi ; dizi adlı değişkenin ilk elemanının adresini bx'e atadık
mov si, 0 ; indexleri gezmek için si yazmacını kullandık
mov cx, 0 ; burada loop kullanmak istemediğim için cx = 0 ataması gerçekleştirdim,
          ; peki loop kullansaydım buraya ihtiyaç var mıydı?
          ; yoksa varsa gene 0 mı olması gerekirdi?
          
karsilastir: ; okunabilirliği arttırmak ve oradan oraya zıplamak için etiket(label)li çalıştık
    mov al, [bx+si]     ; al = dizi[i] buradaki si=i
    inc si              ; i++
    mov dl, [bx+si]     ; dl = dizi[++i]
    cmp al, dl          ; al-dl ? Bayraklara düşecek sonuçlar
    jg  degistir        ; "Jump Greater" ilk işleç daha büyükse atla anlamına gelir: (ZF = 0) ve (SF = OF) 
    jmp bakiver         ; eğer ilk işleç daha büyük değilse "bakiver" etiketine atlanacak
    
degistir:               ; değerleri değiştiriyoruz
    dec si              ; si yazmacındaki değer 1 azalacak
    mov [bx+si], dl     
    inc si
    mov [bx+si], al
    jmp bakiver
    
bakiver:
    mov ax, 4           ; son indexi olan 4
    cmp ax, si          ; si yazmacındaki değer index kontrolu için
    jg karsilastir      ; index kontrolu
    inc cx              ; her tur sonu cx yazmacındaki değer kaçıncı turda olunduğunun kontrolu için
    mov si, cx          ; her tur sonu bir sonraki tur değerinden çizgisel taramaya devam ediyor
    cmp cx, 4           ; son turu olan 4'ü kontrol ediyor 
    jg bitir
    
bitir:
    ret
    
dizi db 1,3,2,5,4       ; byte dizisi - buradaki db ifadesi "DefineByte" anlamına gelmektedir. 
end
```
</p>
</details>


# Yararlı Bağlantılar
- Öykünücü Nedir? https://medium.com/@ozkancakirwork/em%C3%BClat%C3%B6r-nedir-nas%C4%B1l-kullan%C4%B1l%C4%B1r-bbf8a0b5d19a
- Emu8086 indir https://emu8086-microprocessor-emulator.en.softonic.com/
- Emu8086 ve Assembly https://roboturka.com/pic-assembly-pic-c/assembly-ve-emu8086/
- Emu8086 ilk adım https://mimoza.marmara.edu.tr/~ubaspinar/mikro2proje/emu8086_foy.pdf

