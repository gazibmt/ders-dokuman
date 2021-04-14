1.  **İlişkisel Cebir**

SQL dilinin altyapısını oluşturur. Tabloların birbirleri arasındaki ve
tablonun içinde bulunan özelliklerin arasındaki ilişki ile ilgilidir.

  Okul Numarası   TC Kimlik No   İsim     Soyisim   Yaşadığı Şehir
  --------------- -------------- -------- --------- ----------------
  181180077       11111111111    Furkan   Yılmaz    Trabzon
  181180099       22222222222    Neşe     Kambur    Ankara
  181180098       33333333333    Birkan   Ahmetli   Ankara

1.  **Super Key:** Tablodaki bir ya da birden fazla özelliğin birleşince
    tek bir satırı ifade etmesidir. Yani bir super keyden bir tane daha
    bulunamaz. Örneğin tablodaki Okul Numarası + TC Kimlik No + Yaşadığı
    Şehir bir super key oluşturur. Çünkü okul numarası 181180077 olan,
    TC kimlik numarası 11111111111 olan ve yaşadığı şehir Trabzon olan
    bir kişi daha olamaz. Aynı şekilde Okul Numarası + TC Kimlik No +
    Yaşadığı Şehir + İsim ya da Okul Numarası + TC Kimlik No + Yaşadığı
    Şehir + Soyisim de super key oluşturur.

2.  **Candidate Key:** Daha alt super keylere ayrılamayan super keylere
    candidate key denir. Örneğin Okul Numarası + Yaşadığı Şehir tek bir
    kişi için özeldir. Fakat yaşadığı şehre bakmaz ve sadece okul
    numarasıyla ilgilenirsek de o kişinin kim olduğunu anlayabiliriz.
    Yani Okul Numarası + Yaşadığı Şehir daha alt kümelere ayrılıp sadece
    okul numarası olduğunda da bir super key oluşturur. Bu tür super
    keyler candidate keylerdir.

3.  **Primary Key:** Candidate keylerden birinin seçilmesidir. Örneğin
    yukarıdaki örnekte okul numarası da tc kimlik numarası da candidate
    keylerdir. Tablonun amacına göre isteğimiz doğrultusunda bir
    tanesini seçip onu primary key olarak atarız. Candidate keyler
    doğası gereği tablolarda bulunurlar fakat primary keyleri bizler
    tanımlarız. Bir tabloda, birden fazla candidate key bulunabilirken
    yalnızca bir tane primary key bulunur.

```{=html}
<!-- -->
```
2.  **İlişkisel Cebirde Operatörler**

Seçim: $\sigma$ Küme Kesişimi: $\cap$

Projeksiyon: $\mathbf{\Pi}$ Doğal Birleşme:
$\text{Denklemi\ buraya\ yazın.}$

Birleştirme: u Bölme: $\div$

Fark: $-$ Ortalama: avg

Kartezyen Çarpımı: x Minimum: min Maksimum: max

Yeniden Adlandırma:$\text{\ ρ}$ Toplama: sum Eleman sayısı: count

1.  **Seçme Operatörü:**

**r:** $\mathbf{\sigma}_{\mathbf{A = B\ }}$(r): A=B olan her satırı seç

  A   B       C
  --- ------- -------
  1   **1**   **8**
  5   **7**   **0**
  6   **6**   **3**
  2   **3**   **3**
  1   **5**   **8**

  A   B       C
  --- ------- -------
  1   **1**   **8**
  6   **6**   **3**

2.  **Projeksiyon Operatörü**

**r:** $\mathbf{\Pi}_{\mathbf{A,C}}$ **(r):** Sadece A ve C sütunlarını
göster.

  A   B       C
  --- ------- -------
  1   **1**   **8**
  5   **7**   **0**
  6   **6**   **3**
  2   **3**   **3**
  1   **5**   **8**

  A   C
  --- -------
  1   **8**
  5   **0**
  6   **3**
  2   **3**

**Not:** Yeni tabloda tekrarlanan satırlar gösterilmez. (A=1 C=8 ilk
tabloda 1. Ve 5. satırda tekrarlanmış)

3.  **Birleştirme Operatörü**

r: s:

  A   B
  --- -------
  1   **1**
  5   **7**
  6   **6**

  A    B
  ---- -------
  3    **4**
  5    **7**
  10   **6**

r u s: r ve s tabloları birleştirildi. Tekrarlanan satırlar
gösterilmedi. (A=5 ve C=7)

  A    B
  ---- -------
  1    **1**
  5    **7**
  6    **6**
  3    **4**
  10   **6**

4.  **Fark Operatörü**

r: s:

  A   B
  --- -------
  1   **1**
  5   **7**
  6   **6**

  A    B
  ---- -------
  3    **4**
  5    **7**
  10   **6**

  A   B
  --- -------
  1   **1**
  6   **6**

r-s: r tablosu ile s tablosunda ortak olan satırlar silindiğinde oluşan
r tablosudur (A=5 ve B=7).

5.  **Kartezyen Çarpımı**

r: s:

  A   B       C
  --- ------- -------
  1   **1**   **8**
  5   **7**   **0**
  6   **6**   **3**
  2   **3**   **3**

  D    E
  ---- --------
  12   **15**
  27   **7**
  1    **25**

r x s: r ve s tablolarının Kartezyen çarpımıdır.

  A   B       C       D        E
  --- ------- ------- -------- --------
  1   **1**   **8**   **12**   **15**
  1   **1**   **8**   **27**   **7**
  1   **1**   **8**   **1**    **25**
  5   **7**   **0**   **12**   **15**
  5   **7**   **0**   **27**   **7**
  5   **7**   **0**   **1**    **25**
  6   **6**   **3**   **12**   **15**
  6   **6**   **3**   **27**   **7**
  6   **6**   **3**   **1**    **25**
  2   **3**   **3**   **12**   **15**
  2   **3**   **3**   **27**   **7**
  2   **3**   **3**   **1**    **25**

6.  **Örnekler**

> $\mathbf{2.6.1.\ \ }\mathbf{\sigma}_{\mathbf{A > 10\  \land \ B = C\ }}\mathbf{(rxs)}$
> **?**

  C    D
  ---- --------
  8    **19**
  6    **12**
  19   **14**

**r: s:**

  A    B
  ---- --------
  1    **1**
  7    **6**
  19   **8**
  13   **19**

> $\mathbf{\text{rxs}}$**:**

  A    B        C        D
  ---- -------- -------- --------
  1    **1**    **8**    **19**
  1    **1**    **6**    **12**
  1    **1**    **19**   **14**
  7    **6**    **8**    **19**
  7    **6**    **6**    **12**
  7    **6**    **19**   **14**
  19   **8**    **8**    **19**
  19   **8**    **6**    **12**
  19   **8**    **19**   **14**
  13   **19**   **8**    **19**
  13   **19**   **6**    **12**
  13   **19**   **19**   **14**

$\mathbf{\sigma}_{\mathbf{A > 10\  \land \ B = C\ }}\mathbf{(rxs)}$**:**

  A    B        C        D
  ---- -------- -------- --------
  19   **8**    **8**    **19**
  13   **19**   **19**   **14**

> **2.6.2.**
> $\mathbf{\Pi}_{\mathbf{\text{isim\ }}}\mathbf{(}\mathbf{\sigma}_{\mathbf{vize > 60}}\left( \mathbf{\text{notlar}} \right)\mathbf{)}$**?**

Bilgiler:

  Okul Numarası   TC Kimlik No   İsim     Soyisim   Yaşadığı Şehir
  --------------- -------------- -------- --------- ----------------
  181180077       11111111111    Furkan   Yılmaz    Trabzon
  181180099       22222222222    Neşe     Kambur    Ankara
  181180098       33333333333    Birkan   Ahmetli   Ankara
  181180025       44444444444    İrem     Kenar     Manisa
  18118032        55555555555    Özlem    Melek     İzmir

notlar:

  Okul Numarası   Vize   Final   Harf Notu
  --------------- ------ ------- -----------
  181180077       90     100     AA
  181180099       55     100     CB
  181180098       80     70      BB
  181180025       55     40      DD
  18118032        75     70      CB

$\mathbf{\Pi}_{\mathbf{\text{isim\ }}}\mathbf{(}\mathbf{\sigma}_{\mathbf{vize > 60}}\left( \mathbf{\text{notlar}} \right)\mathbf{)}$**:**

  İsim
  --------
  Furkan
  Birkan
  Özlem

7.  **Küme Kesişim Operatörü**

r: s:

  A   B
  --- -------
  1   **1**
  5   **7**
  6   **6**

  A    B
  ---- -------
  3    **4**
  5    **7**
  10   **6**

$$\mathbf{r \cap s}$$

  A   B
  --- -------
  5   **7**

8.  **Doğal Birleşme Operatörü**

9.  **Bölme Operatörü**

**r: s:**

  A    B
  ---- -------
  3    **4**
  5    **7**
  10   **6**
  8    **7**
  9    **3**

  B
  ---
  7

  A
  ---
  5
  8

> **r**$\mathbf{\div s}$**:**

**\
SQL KOMUTLARI**

-   **Create table:** Yeni tablo oluşturmak için kullanılır.

    -   **Kullanımı:** create table tablo_adı (veri_tipi1 özellik1,
        veri_tipi2 özellik2, ..., veri_tipin özellikn)

    -   **Integrity Contraint:** Verinin null olup olamayacağı ve
        primary keyler belirtilir. **Örnek:** create table tablo_adı
        (veri_tipi1 özellik1, veri_tipi2 özellik2, primary key
        (özellik2))

-   **Drop table:** Tabloyu silmek için kullanılır.

```{=html}
<!-- -->
```
-   **Kullanımı:** drop table tablo_adı

```{=html}
<!-- -->
```
-   **Alter table:** Tablo üzerinde değişiklik yapmak için kullanılır.

```{=html}
<!-- -->
```
-   **Add:** Tabloya özellik eklemek için kullanılır.

```{=html}
<!-- -->
```
-   **Kullanımı:** alter table tablo_adı add veri_tipi özellik

```{=html}
<!-- -->
```
-   **Drop:** Tablodan özellik silmek için kullanılır.

```{=html}
<!-- -->
```
-   Kullanımı: alter table tablo_adı drop özellik

```{=html}
<!-- -->
```
-   **Select From:** Tablodan istenen verileri seçmek için kullanılır.

```{=html}
<!-- -->
```
-   **Kullanımı:** select özellik from tablo_adı

-   **\* kullanımı:** tablodaki her özelliği getirir. -\> select \* from
    tablo_adı

> Sorgularda özelliklerle birlikte +, -,/,\* işlemleri de
> kullanılabilir. Bu kullanımlar karıştırılmamalıdır.

-   **Distinct:** Tekrarlamaları engellemek için kullanılır. Örneğin
    adlar sütununda bulunan bütün aynı isimleri tek tek yazmak yerine
    bir kere yazar.

```{=html}
<!-- -->
```
-   **Kullanımı:** select distinct özellik from tablo_adı

```{=html}
<!-- -->
```
-   **All:** Tekrarlamaların kaldırılmayacağını özellikle belirtir.

```{=html}
<!-- -->
```
-   **Kullanımı:** select all özellik from tablo_adı

```{=html}
<!-- -->
```
-   **Where:** Sorgularda koşul belirtir. Örneğin kitap sayfa
    sayılarından oluşan bir sütunda 100den fazla sayfalı kitapların
    isimlerini getirmek istersek select kitap_adı from kitaplar where
    sayfa_sayısı \>100 sorgusunu kullanırız.

```{=html}
<!-- -->
```
-   **Kullanımı:** select özellik from tablo_adı where koşul

-   **And, or, not kullanımı:** select özellik from tablo_adı where
    koşul1 and koşul2

```{=html}
<!-- -->
```
-   **Delete:** Satır veya satırları silmek için kullanılır.

```{=html}
<!-- -->
```
-   **Kullanım:** delete from tablo_adı where koşul

```{=html}
<!-- -->
```
-   **Insert Into:** Satır eklemek için kullanılır.

```{=html}
<!-- -->
```
-   **Kullanım:** insert into tablo_adı (özellik1, özellik2, özellik3)
    values (veri1, veri2, veri3)

```{=html}
<!-- -->
```
-   **Update:** Mevcut bir satırdaki verileri değiştirmek için
    kullanılır.

```{=html}
<!-- -->
```
-   **Kullanım:** update tablo_adı set özellik=özellikte yapılacak
    değişiklik where koşul

```{=html}
<!-- -->
```
-   **As: Özellikleri yeniden adlandırmak için kullanılır.**

    -   **Kullanım:** select özellik as yeni_ad from tablo_adı

-   **Like:** İçinde istenen string bulunan verileri getirir.

```{=html}
<!-- -->
```
-   **Kullanım:** select özellik from tablo_adı where
    aranan_kelimenin_bulunduğu_özellik like '%aranan_kelime%'

```{=html}
<!-- -->
```
-   **Order by:** Tablodaki satırları sıralamak için kullanılır. Örneğin
    yaş özelliğinin bulunduğu bir tabloda kişileri küçükten büyüğe order
    by kullanarak sıralayabiliriz.

```{=html}
<!-- -->
```
-   **Kullanım:** select özellik from tablo_adı where koşul order by
    sıralamak_için_kullanılacak_özellik

```{=html}
<!-- -->
```
-   **Union:** Tablolardaki istenen özellikleri birleştirmek için
    kullanılır.

```{=html}
<!-- -->
```
-   Kullanım: (select özellik from tablo_adı) union (select özellik from
    diğer_tablo_adı)

```{=html}
<!-- -->
```
-   **Intersect:** Sorgulardaki ortak olan satırları bulur.

```{=html}
<!-- -->
```
-   Kullanım: (select özellik from tablo_adı) intersect (select özellik
    from diğer_tablo_adı)

```{=html}
<!-- -->
```
-   **Except:** İlk sorgudan iki sorguda ortak bulunan satırları
    çıkarır.

```{=html}
<!-- -->
```
-   **Kullanım:** (select özellik from tablo_adı) except (select özellik
    from diğer_tablo_adı)

```{=html}
<!-- -->
```
-   **Aggregate Fonksiyonları:** İstenen özellik için avg (ortalama),
    min(minimum), max (maksimum), sum (toplama), count (sayısı)
    değerlerini bulur.

```{=html}
<!-- -->
```
-   **Kullanım:** select count (özellik) from tablo_adı

```{=html}
<!-- -->
```
-   **Group By:** Seçilen özelliğe göre gruplama yapar. Örneğin bir
    öğrenci veri tabanında notlara göre gruplanmak istendiğinde her harf
    notu için o notu alan öğrenciler tek bir satırda sıralanır.

```{=html}
<!-- -->
```
-   **Kullanım:** select özellik from tablo_adı where koşul group by
    özellik

```{=html}
<!-- -->
```
-   **Having:** Where ile amacı aynıdır. Group by kullanılıyorsa having
    kullanılır.

```{=html}
<!-- -->
```
-   **Kullanım:** select özellik from tablo_adı group by özellik having
    koşul

```{=html}
<!-- -->
```
-   **Some:** Tablo karşılaştırmalarında koşul ile kullanılır.
    Karşılaştırmaların hepsinde değil de bazılarında koşulu sağlamasının
    yeterli olduğu durumdur.

    -   **Kullanım:** select özellik from tablo_adı where özellik\> some
        (select özellik from tablo_adı where koşul)

-   **Unique:** Tekrarı olmayan verilerin gösterilmesini sağlar.

    -   **Kullanım:** select özellik from tablo_adı where unique (select
        özellik from tablo_adı where koşul)

```{=html}
<!-- -->
```
-   **Create index:** Primary keyler kendileri doğal olarak birer indeks
    oluştururlar fakat bunu özel olarak biz de oluşturabiliriz.

```{=html}
<!-- -->
```
-   **Kullanım:** create index indekse_verilecek_isim on
    tablo_adı(özellik)

```{=html}
<!-- -->
```
-   **Create type:** Typedef'e benzer şekilde yeni bir veri tipi
    oluşturulmasını sağlar.

-   **Create domain:** Create type ile benzerdir fakat domainlerde ek
    olarak constraitleri de tanımlayabiliyoruz.

**Views**

Oluşturulan geçici tablolara views denir. Tablolar diskte yer kaplarken
viewlar kaplamaz. Kullanıcılara tablolar yerine viewlara erişim vermek
daha güvenlidir. Yer kaplamamak adına bir sorgunun viewu oluşturulur ve
tekrar tekrar o sorguyu yazmak yerine viewdan bakabiliriz.

-   **Kullanım:** create view isim as \<sorgu\>

1.  **İşlemler (Transactions)**

> **Commit:** Veri tabanı diskte fazla yer kaplamamak amacı ile bütün
> verileri hemen diske yazmıyor, bunun yerine hafızada geçici bir
> bellekte tutuyor. Bu geçici hafızada bulunan verileri diske yazmak
> için commit komutunun verilmesi gereklidir. Bu komut, algoritmaya
> bağlı olarak (örn: 5 işlem sonrası commit et) kendi de commit
> edilebilir, commit komutunu bizim vermemiz de gerekebilir. Bu işlem
> yapılmazsa, veriler eğer diske yazılmazsa kaybolur. Çoklu ortamlarda
> verilerin güncel kalmasını sağlar.
>
> **Rollback:** Commit edilen (kaydedilen) her işleme geri dönüş
> sağlanmasını sağlar.

2.  **Integrity Constraint**

> Veri tabanı için bazı şartlar konulmasını sağlar. Bunlardan 4 tanesi:

-   **Not null:** Birlikte belirtildiği özelliğin boş bırakılamayacağını
    belirtir. Örneğin öğrenci bilgilerini tutan bir sistemde tabloda
    öğrenci numarasının boş bırakılamaması bu ifadeyle sağlanır.

-   **Primary Key:** Candidate keylerden birinin seçilmesidir. Yani
    tekrarlanan satırlardan değil sadece eşi olmayan satırlardan oluşan
    özelliklerden birinin seçimidir. Tablonun amacına göre seçilir.
    Öğrenci bilgi sistemindeki öğrenci numarası buna örnek olarak
    verilir.

-   **Unique:** Bu şart, tabloda bulunan verilerin tekrarının
    bulunmamasını, o sütunda o veriden sadece bir tane bulunmasını
    zorunlu tutar.

-   **Check:** Verilen şartı kontrol eder. Örneğin bir özellik için
    sadece 3 farklı yazılabilecek seçenek varsa bundan farklı bir veri
    girildiğinde constraint hatasının verilmesi sağlanır. Bu seçenekler
    manuel olarak da belirtilebilir ((check (özellik in (seçenek2,
    seçenek2, seçenek3)) yani o özellik için bu 3 veriden biri
    girilebilir başka veriler kabul edilmez.), ya da tablo şeklinde de
    tutulup o tabloda bulunan verilerden birinin girilmesi şart
    koşulabilir.

3.  **Referential Integrity**

> Birbiri ile bağlantılı tablolarda, bir tablo diğerinden verileri
> kullanıyorsa ve eğer o tabloda veriler silinirse bir problem ortaya
> çıkar. **Foreign key**, bir tablonun primary keyinin başka bir tabloda
> yer almasıdır. Yani bir tablonun primary keyi ile diğerinin foreign
> keyi ilişkilendirilir. Örneğin öğrenci için yeni bir ders programı
> tablosu oluşturduğumuzu var sayalım:
>
> Öğrenci_id varchar(20)
>
> Foreign key (öğrenci_id) reference öğrenci_bilgileri
>
> On delete cascade
>
> On update cascade
>
> Öğrenci_bilgileri tablosundaki primary key olan öğrenci_id'yi yeni
> tablomuzda direkt olarak kullanmak için reference ile foreign key
> oluşturduk. On delete cascade, on update cascade ile de
> öğrenci_bilgileri adlı tabloda olası değişimler için (silme ve
> güncelleme) kontrol sağladık.

4.  **Yetkilendirme (Authorization)**

> Herkesin veri tabanı üzerinden değişiklik yapabilmesi güvenli değildir
> bu yüzden kısıtlandırılmalıdır. Bunun için:

-   Veri tabanı üzerinde:

```{=html}
<!-- -->
```
-   Delete (Silme)

-   Update (Güncelleme)

-   Read (Okuma)

-   Insert (Ekleme)

```{=html}
<!-- -->
```
-   Veri tabanı şeması üzerinde:

```{=html}
<!-- -->
```
-   Index (İndis ekleme, çıkarma)

-   Resources (Yeni ilişki yaratma)

-   Alteration (Değişiklik yapma)

-   Drop (İlişkilerin silinmesi)

Gibi yetkileri biz kullanıcılara veririz. Bu yetkileri ise **grant**
komutu ile veririz.

-   **Kullanımı**: grant \<verilecek yetkilerin listesi\> on \<tablo
    ismi\> to \<yetki verilecek kişilerin listesi\>

**Revoke** ise yetkileri geri almak için kullanılır.

-   **Kullanımı**: revoke \<alınacak yetkilerin listesi\> on \<tablo
    ismi\> from \<yetki alınacak kişilerin listesi\>

**Entity Relationship Diagram**

![](media\image1.png){width="2.9923611111111112in"
height="3.18125in"}**Entity:** Kendine ait özellikleri olan nesnelerdir.
Örneğin öğrenci veri tabanındaki öğrenci bir entitydir.

**Özellik:** Öğrenci entitysine ait öğrenci numarası, ismi, e-maili
örnek verilebilir.

**Zayıf entity:** İki entityden biri diğeri olmadan var olamıyorsa buna
zayıf entity denir. Zayıf olmayanda bulunan bilgilerden, zayıf olanın
bilgilerine ulaşılabilir. Primary keye ihtiyaçları yoktur, zayıf
olmayanın primary keyi zayıf olanın da primary keyidir.

**Çok değerli özellik:** Aynı özellik başlığı altında birden fazla değer
alabilen özelliklerdir. Öğrenci sisteminde öğrencinin aldığı dersler
örnek verilebilir. Alınan dersler başlığı altında bir ders de olabilir,
birden fazla ders de bulunabilir.

**İlişki:** Entityler arasındaki ilişkiyi gösterir.

**Türetilen Özellik:** Başka özelliklerden de anlaşılabilen, gerekli
olmayan özelliklerdir. Örneğin öğrenci sisteminde öğrencinin doğum
tarihi ve yaşı diye iki özellik olduğunda yaşı türetilen bir özellik
diyebiliriz. Tablodan yaşın çıkarılması sorun olmayacaktır çünkü doğum
tarihinden yaşı elde edilebilir.

**Zayıf Entity için İlişki:** Bir entity ile zayıf bir entity arasındaki
ilişkiyi gösterir.

**Bağımlı Entity:** Varlığı farklı bir entitye bağlı olan entitylerdir.
Örneğin banka sisteminde müşteri ve borç adında iki entityden borç zayıf
entitydir. Müşteri zorunlu bir öğedir fakat her müşterinin borcu olmak
zorunda değildir. Müşteri yoksa borçtan bahsedemeyiz fakat borcu olmayan
müşteriler de bulunur.

**Zayıf Entity için Primary Key:** Zayıf entitylerin primary keylere
ihtiyacı olmasa da bir primary key belirtilebilir.

**ISA:** Kalıtım gibi düşünülebilir. Bir insan entitysinin ISA ile
bağlantısının altında çalışan ve müşteri adında iki entity verilmesi
örnek verilebilir. Çünkü çalışanlar da müşteriler de insandır ("...is
a...").

**One to one:** Bire bir ilişkilerdir. Evli olan eşlerin ilişkisi örnek
verilebilir. Bir kişinin sadece bir tane eşi olabilir. Veri tabanında
tek bir tabloya indirgenebilirler.

**One to Many- Many to One:** Bir danışman öğretmenin birden fazla
öğrencisi varken bir öğrencinin tek bir danışmanı olması many to onea
örnek verilebilirken bu ilişkiye diğer açıdan bakıldığında bir
öğrencinin bir danışman öğretmeni varken bir danışman öğretmenin birden
fazla öğrencisi olması da one to many durumudur.

**Many to Many:** Sıkıntılı ilişkilerdir. Bu ilişkilerle
karşılaşıldığında amaç bunları one to many/many to onea indirgemek
olmalıdır. Bir öğrenci birden fazla ders alırken, bir derste de birden
fazla öğrenci bulunması bu duruma örnektir.

**ERD Örneği:**

![](media\image2.png){width="6.21875in" height="2.0104166666666665in"}

-   Loan (borç): entity

-   Payment (ödeme): Zayıf entity

-   Loan_payment (borç ödeme): zayıf entity için ilişki

-   Loan_number (borç numarası): primary key

-   Payment_number (ödeme numarası): zayıf entity için primary key

-   Amount (miktar), payment_date (ödeme tarihi), payment_amount (ödeme
    miktarı): özellik

Burada ödeme zayıf entityken borç zayıf olmayan entitydir. Ödeme için
olan bütün bilgilere borç entitysinden de ulaşılabilir. Ödeme bağımlı
bir entitydir. Çünkü borç ödeme olmadan da var olabilir fakat ödeme
ancak borç olduğu zaman yapılır. Borç ile ödemenin arasındaki ilişki
borç ödeme ilişkisidir ve zayıf entity bulunduğu için zayıf ilişkidir.
Borç ile ödeme arasındaki ilişki ise one to manydir, bir borcun birden
fazla ödemesi bulunabilir fakat her ödeme tek bir borca aittir.
