Git Nedir? Neden Kullanılır?
----------------------------
----------
Git bir versiyon kontrol sistemidir. Bu sistem sayesinde, bir projede aynı anda birden fazla kişi
çalışabilir ve bir dosyada yapılan tüm değişiklikler (history) görüntülenebilir. 

Diyelim ki *a.html* dosyasına yeni kodlar yazdınız. Ancak daha sonra bu kodların beklediğiniz gibi çalışmadığını gördünüz ve bu değişiklikleri geri almak istediniz. Normalde olsa tek tek eklediğiniz satırları elle silmeniz  gerekirdi. Ama Git sayesinde “BU DOSYAYI ŞU TARİHTEKİ HALİNE GERİ DÖNDÜR” diyebiliyorsunuz. Yani dosyayı eski haline (eski bir versionuna) dönüştürebiliyorsunuz. Git kodlarınızda her değişiklik yapıp bu değişiklikleri *commit ettiğinizde* o dosyadaki değişikliklerinizin bir fotoğrafını çeker ve deponuza (*repository*) kaydeder. Böylece istediğiniz dosyada istediğiniz tarihteki değişikliği görüntüleyebilirsiniz.


Ayrıca Git kullanmanız takım çalışmasını inanılmaz bir şekilde kolaylaştırıyor ki bu konuya **Git ile ekip çalışması** başlığında değineceğiz

Bu noktada bazı terimlerden bahsetmekte fayda var.
(*anlamadıysanız endişelenmeyin aşağıda detaylı bir örnek bulacaksınız*)

 1. repository : (kod deposu) Tüm kodlarınızın tarihçelerinin barındırıldığı depodur. Proje dizininizde **git init** komutu çalıştırılarak o dizinde bir repository oluşturulabilir.
 2. working directory : (çalışma alanı) Projenizin ana dizinidir. Bir dosyanın working directory'de bulunması o dosyanın **git** tarafından takip edildiği manasına gelmez. Sadece **staging area**'daki dosyalar git tarafından takip edilir.
 3. staging area : **git** tarafından takip edilen dosyalar bu alanda bulunur. Bu gerçek manada fiziki bir alan / klasör değildir. Dosyalarınızın durumunu belirten hayali bir etikettir. 
 4. commit : (taahhüt) bir dosyada yaptığınız değişikliklerin kalıcı değişiklikler olduğunun taahhüdü vermeniz gerekir. Böylece o dosyada yaptığınız değişiklikler repository'nize kaydedilir.

**Örnek**
Bir projeniz olduğunu varsayalım. C++ ile hesap makinası yapıyorsunuz. Bu bir c++ eğitimi olmadığı için kodları minimum seviyede tutma amacıyla header vs gibi detayları yazmayacağım.

**hesapmak** klasöründe main.cpp dosyanızın şöyle bir içeriği olduğunu düşünün:

    void main() {
        printf("Hello Git!");
    }

Şimdi bu uygulamanızı Git ile takip edebilmeniz için hesapmak klasöründe bir git repo'su oluşturmalısınız. Terminalinizde hesapmak klasörüne gidip bu komutu çalıştırın:

git init

Artık bu klasördeki tüm dosyalar git ile takip edilebilir haldeler (henüz takip edilmiyorlar!)

Şimdi `git status` komutu çalıştırın.

![enter image description here][1]

**git** main.cpp dosyamızı gördü ama *Untracked* yani henüz takip edilmiyor. Yani sadece çalışma alanımızda (working directory) . Şimdi git'e "Bu dosyaya takip et!" dememiz yani Staging Area'ya almamız gerekiyor.

    git add main.cpp

tekrar repomuzun durumuna bakalım.

![enter image description here][2]

Artık git bu dosyamızı takip ediyor ve bize diyor ki bu dosyada bazı değişiklikler var ama henüz commit edilmemiş. Hemen commit edelim.

    git commit -m 'bu benim commit mesajım'

![enter image description here][3]

Tebrikler ilk commitiniz! :) Git main.cpp dosyanızın o anki halini kaydetti. Şimdi main.cpp dosyanızda rastgele değişiklikler yapın. Diyelim ki bazı değişiklikler yaptınız, birşeyler denediniz ama istediğiniz sonuçları alamadınız, kodunuz çalışmıyor, töbe yarabbi acayip acayip birşeyler oldu. TÜm değişiklikleri silip son çalışır haline yani en son commitinizdeki haline geri döndürmek istiyorsunuz. Önce bir `git status`deyip hangi dosyalarda değişiklik var ne olmuş ne bitmiş bir bakalım

![enter image description here][4]

**main.cpp** değiştirilmiş ama henüz commit edilmemiş. Biz bu değişiklikleri hemen geri alalım. `git status`komutu bize bunu nasıl yapacağımızı da söylüyor zaten (ekran görüntüsü 5. satır)

    git checkout -- main.cpp

Şimdi main.cpp dosyanızı açtğınızda yaptığınız değişikliklerin gittiğini ve dosyanın son committeki haline döndüğünü göreceksiniz. Tekrar `git status` diyerek kontrol edebilirsiniz. Şimdi main.cpp'de tekrar değişiklikler yapın ve diyelim ki bu değişiklikler canavar gibi çalışıyor ve dosyanın bu halini saklamak istiyorsunuz. Tekrar git status ile kontrol edebilirsiniz. Dosyayı yine `git add main.cpp` ile commit edilecekler listesine ekliyoruz ve daha sonra commit ediyoruz.

![enter image description here][5]

Farkettiyseniz dosyanın sadece çalışır ve memnun olduğumuz hallerini commit ettik. Bu nokta çok önemli. **Her zaman dosyalarınızın nihai, çalışır hallerini commit edin.** 

Dosyanızda hangi tarihte ne değişiklikler yaptığınızı merak ederseniz istediğiniz commite geri dönebilirsiniz. Bunun için önce commitlerimizi listeleyelim.

    git log

![enter image description here][6]

Şimdi bakalım ilk committen sonra ne değişiklikler olmuş? Commitin ID'sini (benimki 801a... diye gidiyor, sizinki farklı olacaktır)

    git diff 801a786096c84596ff13a1f86759cc99d4ef1607

![enter image description here][7]

Gördüğünüz gibi, ilk commitimde main.cpp dosyası boştu ve ben daha sonra ilk satıra **asdasd** yazmışım. 

İlk committeki haline geri dönmek istediğiniz varsayalım.

    git checkout 801a786096c84596ff13a1f86759cc99d4ef1607

Artık main.cpp ilk committeki haline döndü. Tekrar en son committeki haline geri döndürmek için aynı komutu kullanabilir ya da kısaca `git checkout master` diyebilirsiniz. Aslında manası daha derin olsa da şimdilik `master`'ın son commitinizi ifade ettiğini söyleyebilirim.

**Editör Notu **
Burada bir hatam oldu ve daha anlaşılır olsun diye commit mesajlarında "ilk mesajım" gibi ifadeler kullandım. Normalde böyle anlaşılmaz mesajlar gönderdiğinizde çalışma arkadaşlarınızdan dayak yiyebilirsiniz. Çünkü bu mesajlar çok önemli. Mesajlarda her zaman o committe ne değişiklik yaptığınızı, hangi bug'ı düzelttiğiniz yazmalısınız ki yarın öbür gün "ben hangi committe şu hatayı düzeltmiştim yahu?!" diye debelenmeyin. Birkaç commit mesajı örneği vermek gerekirse :

"Kullanıcıdan veri talep edilen fonksiyon yazıldı"
"Artık scanf yerine cin kullanılıyor"
"Kullanıcının sayı yerine harf girmesi engellendi"
"15 nolu bug düzeltildi"
 
Pull / Push kavramları farkları ve kullanım yerleri
---------------------------------------------------
----------

Şu ana kadar hep kendi bilgisayarımızda çalıştık, dosya düzenledik, ekledik, sildik oyunlar oynadık. Yani hep localdeydik. Peki ama bu git repomuzu uzaktaki bir sunucuya yedekleyemez miyiz? Bu GitHub, BitBucket nedir? İn midir cin midir biraz onlardan bahsedelim. Bunun için remote repo kavramından bahsedeyim, en basit tanımıyla localinizdeki reponuzun uzak bir sunucudaki kopyasıdır. Başka insanların reponuzu görebilmesi, kodlarınızı (siz isterseniz) görebilmesi ve indirebilmesi için bu kodları bir sunucuya koymak gerekir. Bu amaçla kendiniz bir sunucu kiralayıp, o sunucuya da bir **git** kuabilirsiniz, ya da bunlarla hiç uğraşmayıp GitHub ya da BitBucket kullanabilirsiniz. Bu 2 servis de tam olarak yukarıda anlattığım işi yapıyorlar. 

Hemen github.com adresine girip üye olup **new repository** diyerek yeni bir repository oluşturalım.

![enter image description here][8]

Şimdi local repomuza "Artık bu reponun remote adresi şudur, commitlerimi o adrese **de** gönder" diyebilmemiz için localimzdeki repoya github repo adresimizi ekliyoruz.

git remote add origin https://github.com/erayalakese/Hesap-Mak.git

Bu komut ile remote repomuzu da local repomuza tanıttıktan sonra localimizdeki tüm commitlerimizi remote'a göndermeliyiz. Bu işleme **push** adı veriliyor, yani localimizdeki commitleri remote'a *itiyoruz* .

    git push origin master

![enter image description here][9]

Artık tüm commitlerinizi GitHub'da da görebilirsiniz. Ancak localinizde yaptığınız tüm commitler remote'a otomatik olarak push **edilmiyor** . Bu yüzden commit ettikten sonra git push komutunu tekrar çalıştırmalısınız. Her commit sonrası push etmenize gerek yok, commitlerinizi localinizde biriktirip gün sonunda toplu olarak push edebilirsiniz.

`pull` komutu ise `push` komutunun tam tersini yapıp sunucudaki commitleri local reponuza çekmeye yarar ancak şuan tek geliştirici siz olduğunuz için localinizdeki repo ile remote repo aynı olacaktır. Dolayısıyla pull ettiğinizde size sunucudan hiçbir commit gelmeyecektir. `pull` komutunu başka developerların sizin reponuza gönderdiği commitleri localinize çekmeniz için kullanacağız. Detayları **Git ile ekip çalışması** başlığında göreceksiniz.

Git ile ekip çalışması
----------------------
----------

Bu noktaya kadar hep kendi kendimize oyunlar oynadık, eğlendik. Peki ama projenin tek geliştirici biz değilsek ne olacak? Diğer developer kardeşler nasıl commit yollayacak? Nasıl değişiklik yapacak? Bu değişiklikleri biz nasıl göreceğiz? İşte bu noktada **git** hayatımızı kurtarıyor. 

Remote sunucumuz diğer developerlar ile aramızdaki köprü olacak. Biz değişiklik yapıp commit edip sunucuya yollayacağız, diğer developerlar pull edip o değişiklikleri sunucudan alacaklar, sonra onlar commit yollayacak biz pull edip o değişiklikleri sunucudan alacağız. Ne kadar kolay değil mi? Değil. ( conflict <3 )

Diyelim ki bir diğer developer bazı değişiklikler yapıp sunucuya commit push etti. Ama bizim henüz bundan haberimiz yok. Biz efendi efendi kendi localimizde çalışıyor, değişiklikler yapıyoruz. Commitlerimizi yaptık, sunucuya push edeceğiz, ama o da ne?!
![enter image description here][10]

Push talebimiz reddedilmiş, çünkü bir başkası bizden önce sunucuya birşeyler push etmiş. **git** de bize diyor ki, "bak başkaları birşeyler gönderdi, önce onları bilgisayarına al, bir bak bakalım, daha sonra sen kendi commitlerini push edersin".

Biz de `git pull origin master` diyerek sunucudaki commitleri localimize pull ediyoruz (çekiyoruz) . Bu commiti çalıştırınca şöyle bir ekran gelecek : 

![enter image description here][11]

Burada olanları size şöyle anlatayım, diğer developerın yaptığı değişiklikler ile sizinkiler birleştiriliyor, yani **merge** ediliyor ve bu merge işlemi için bir mesaj (aynı commit mesajı gibi) girmeniz isteniyor. Otomatik olarak gelen mesajı kabul edebilirsiniz, nano adlı editör kullanıldığı için sırasıyla şu tuşlara basabilirsiniz : **ESC , :wq, ENTER**

Artık diğer developer'ın yaptığı değişiklikler de sizin localinizde, şimdi push dediğinizde kendi değişikliklerinizi de sunucuya gönderebilirsiniz. `git log`komutunu çalıştırınca neler olduğunu daha iyi anlayacaksınız (aşağıdan yukarıya doğru okuyun) :

![enter image description here][12]

Ben "eklemeler yapıldı" şeklinde bir commit yapmışım, tam sunucuya gönderecekken Özgür benden önce bir commit (deneme dosyası eklendi) push etmiş. Dolayısıyla ben önce Özgür'ün commitini localime aldım, merge ettim, daha sonra kendi commit'imi sunucuya gönderdim. Böylece ikimizin de yaptığı değişiklikler sunucuya gönderilmiş oldu. Özgür ne değişiklik yapmış bir bakalım :

![enter image description here][13]

Özgür deneme.cpp adında yeni bir dosya oluşturmuş (new file mode), `ls` komutu çalıştırınca bu dosyanın da bana geldiğini görebilirsiniz.

Bu şekilde yüzlerce, binlerce developer birlikte çalışabilirsiniz. Siz uygulamanın bir modülü üzerinde çalışırken, bir başkası farklı bir modülü üzerinde çalışabilir ve kolayca diğer developerların değişikliklerini kendi bilgisayarınıza alabilirsiniz.

Conflict / Merge kavramları
---------------------------
----------

Detaylı Kaynaklar
-----------------
----------


 1. [http://git-scm.com/book/][14]

> Written with [StackEdit](https://stackedit.io/).


  [1]: http://cl.ly/image/1j1d0E0b273C/Image%202014-08-13%20at%203.39.05%20%C3%96S.png
  [2]: http://cl.ly/image/3F3i3a1j3i13/Image%202014-08-13%20at%203.42.10%20%C3%96S.png
  [3]: http://cl.ly/image/3Z3u13282Y3b/Image%202014-08-13%20at%203.44.20%20%C3%96S.png
  [4]: http://cl.ly/image/2L0l1l0i1p0p/Image%202014-08-13%20at%203.47.20%20%C3%96S.png
  [5]: http://cl.ly/image/1f1k1r103v3C/Image%202014-08-13%20at%203.53.55%20%C3%96S.png
  [6]: http://cl.ly/image/2O3L1X2v3R3k/Image%202014-08-13%20at%203.57.53%20%C3%96S.png
  [7]: http://cl.ly/image/0r2m3O0D2y3c/Image%202014-08-13%20at%204.00.51%20%C3%96S.png
  [8]: http://cl.ly/image/2V0J0i0c1r21/Image%202014-08-13%20at%204.22.00%20%C3%96S.png
  [9]: http://cl.ly/image/1V3t0H3t1T3U/Image%202014-08-13%20at%204.27.09%20%C3%96S.png
  [10]: http://i.imgur.com/bbkQQxy.png
  [11]: http://i.imgur.com/fw3buIN.png
  [12]: http://i.imgur.com/JZlgbO1.png
  [13]: http://i.imgur.com/Qq0hes4.png
  [14]: http://git-scm.com/book/