# Git Kullanım Rehberi

### Conflict/Merge

Ekip çalışması başlığında farklı dosyalar üzerinde nasıl çalışabileceğinizi anlatmıştım. Ancak diğer developerlar sizinle aynı dosya üzerinde çalışıyorsa ne olacak? Sizin eklediğiniz bir satırı bir başkası silerse ne olacak? Hanginizinki kullanılacak? Bu soruları bu başlıkta cevaplayacağım. 

Diyelim ki `main.cpp` dosyasının 1. satırında bazı değişiklikler yapıp bu değişiklikleri commit ettim. Aynı anda da Özgür de aynı dosyanın 2. satırını değiştirdi, benden önce commit ederek sunucuya push etti. Ama benim bundan haberim yok tabi ki. Ben kendi commitimi push etmek istediğimde ne olacak görelim :

![enter image description here][14]

Daha önce de bu hatayı görmüştük, birisinin bizden önce sunucuya push ettiğini gösteriyor. Biz de `git pull` deyip önce o değişiklikleri çekmeye çalışalım.

![enter image description here][15]

Evet bu sefer pull ettiğimizde Özgür'ün değişiklikleriyle benim değişikliklerimi birleştiremedi (Merge) . Çünkü aynı dosyada değişiklik yaptık ve farklı commitlerle aynı dosyanın farklı hallerinin doğru olduğunu iddia ettik. **git** de bize diyor ki, "E şimdi ben hangisini kullanayım? Çakışma (Conflict) var. Bunu çöz, öyle commit et!" . Hemen `main.cpp` dosyamıza bakıyoruz.

Dosyanın değişiklikler yapılmadan ve ben son commitimi yapmadan önceki hali;

```
asdasd
eklemeler
```

Dosyanın pull denemesi yaptıktan sonraki hali;

```
    <<<<<<< HEAD
    eray değiştirdi
    eklemeler
    =======
    asdasd
    özgür değiştirdi
    >>>>>>> 022380c1eae898dbd30e22bd02bd708e2609599a
```

Burada **<<<<<< HEAD** ile **======** arasındaki kodlar benim yaptığım değişiklikler, **======** ile **>>>>> COMMIT ID** arasındaki kodlar ise Özgür'ün yaptığı değişiklikler. Ben 1. satıra **eray değiştirdi** yazmışım, Özgür ise 2. satıra **Özgür değiştirdi** yazmış. Şimdi benim burada Özgür ile de görüşüp, bu dosyanın son halini oluşturmam gerekiyor. Son halini şöyle düzenledim (<<<< ve >>>> gibi ifadeleri silerek)

```
    eray değiştirdi
    özgür değiştirdi
```

şimdi tekrar `git status` diyelim bakalım.
![enter image description here][16]

Bize diyor ki, main.cpp dosyası merge edilmemiş, conflict'i çöz (zaten çözdük) ve sonra git add komutu ile bunu yeniden commit edilecekler listesine ekleyip commit edelim.

![enter image description here][17]

İşte bu kadar :) Conflict'i çözdük ve main.cpp'nin en doğru halini sunucuya push ettik. Özgür pull ettiği zaman dosyanın en güncel halini alacak.

  [14]: http://i.imgur.com/B7p67vM.png
  [15]: http://i.imgur.com/eUDoWl8.png
  [16]: http://i.imgur.com/6Gn6oHm.png
  [17]: http://i.imgur.com/6rg1Yys.png
  