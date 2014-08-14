# Git Kullanım Rehberi

### Pull&Push

Şu ana kadar hep kendi bilgisayarımızda çalıştık. Dosya düzenledik, ekledik, sildik, oyunlar oynadık. Yani hep localdeydik. Peki ama bu git repomuzu uzaktaki bir sunucuya yedekleyemez miyiz? Bu GitHub, BitBucket nedir? İn midir cin midir biraz onlardan bahsedelim. 

Bunun için `remote repo` kavramından bahsetmek gerek. En basit tanımıyla localinizdeki reponuzun uzak bir sunucudaki kopyasıdır. Başka insanların reponuzu görebilmesi, kodlarınızı (siz isterseniz) görebilmesi ve indirebilmesi için bu kodları bir sunucuya koymak gerekir. Bu amaçla kendiniz bir sunucu kiralayıp, o sunucuya da bir **git** kurabilirsiniz. Ya da bunlarla hiç uğraşmayıp GitHub ya da BitBucket kullanabilirsiniz. Bu 2 servis de tam olarak yukarıda anlattığım işi yapmaktadır. 

Hemen GitHub.com adresine girip, üye olarak **new repository** direktifiyle yeni bir repository oluşturalım.

![enter image description here][8]

Şimdi local repomuza "Artık bu reponun remote adresi şudur, commitlerimi o adrese **de** gönder" diyebilmemiz için localimzdeki repoya github repo adresimizi ekliyoruz.

```
git remote add origin https://github.com/erayalakese/Hesap-Mak.git
```

Bu komut ile remote repomuzu da local repomuza tanıttıktan sonra localimizdeki tüm commitlerimizi remote'a göndermeliyiz. Bu işleme **push** adı veriliyor, yani localimizdeki commitleri remote'a *itiyoruz* .

```
git push origin master
```

![enter image description here][9]

Artık tüm commitlerinizi GitHub'da da görebilirsiniz. Ancak localinizde yaptığınız tüm commitler remote'a otomatik olarak push **edilmiyor** . Bu yüzden commit ettikten sonra git push komutunu tekrar çalıştırmalısınız. Her commit sonrası push etmenize gerek yok. Commitlerinizi localinizde biriktirip gün sonunda toplu olarak push edebilirsiniz.

`pull` komutu ise `push` komutunun tam tersini yapıp sunucudaki commitleri local reponuza çekmeye yarar ancak şuan tek geliştirici siz olduğunuz için localinizdeki repo ile remote repo aynı olacaktır. Dolayısıyla pull ettiğinizde size sunucudan hiçbir commit gelmeyecektir. `pull` komutunu başka developerların sizin reponuza gönderdiği commitleri localinize çekmeniz için kullanacağız. Detayları **Git ile ekip çalışması** başlığında göreceksiniz.

[8]: http://cl.ly/image/2V0J0i0c1r21/Image%202014-08-13%20at%204.22.00%20%C3%96S.png
[9]: http://cl.ly/image/1V3t0H3t1T3U/Image%202014-08-13%20at%204.27.09%20%C3%96S.png
