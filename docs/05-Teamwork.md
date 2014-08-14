# Git Kullanım Rehberi

### Ekip Çalışması

Bu noktaya kadar hep kendi kendimize oyunlar oynadık, eğlendik. Peki ama projenin tek geliştirici biz değilsek ne olacak? Diğer developer kardeşler nasıl commit yollayacak? Nasıl değişiklik yapacak? Bu değişiklikleri biz nasıl göreceğiz? İşte bu noktada **git** hayatımızı kurtarıyor. 

Remote sunucumuz diğer developerlar ile aramızdaki köprü olacak. Biz değişiklik yapıp commit edip sunucuya yollayacağız, diğer developerlar pull edip o değişiklikleri sunucudan alacaklar. Sonra onlar commit yollayacak, biz pull edip o değişiklikleri sunucudan alacağız. Ne kadar kolay değil mi? Değil. ( conflict <3 )

Diyelim ki bir diğer developer bazı değişiklikler yapıp sunucuya commit, ardından push etti. Ama bizim henüz bundan haberimiz yok. Biz efendi efendi kendi localimizde çalışıyor, değişiklikler yapıyoruz. Commitlerimizi yaptık, sunucuya push edeceğiz, ama o da ne?!
![enter image description here][10]

Push talebimiz reddedilmiş, çünkü bir başkası bizden önce sunucuya birşeyler push etmiş. **git** de bize diyor ki; "Bak başkaları birşeyler gönderdi, önce onları bilgisayarına al, bir bak bakalım, daha sonra sen kendi commitlerini push edersin".

Biz de `git pull origin master` diyerek sunucudaki commitleri localimize pull ediyoruz(Çekiyoruz). Bu commiti çalıştırınca şöyle bir ekran gelecek : 

![enter image description here][11]

Burada olanları size şöyle anlatayım; diğer developerın yaptığı değişiklikler ile sizinkiler birleştiriliyor. Yani **merge** ediliyor ve bu merge işlemi için bir mesaj (aynı commit mesajı gibi) girmeniz isteniyor. Otomatik olarak gelen mesajı kabul edebilirsiniz, nano adlı editör kullanıldığı için sırasıyla şu tuşlara basabilirsiniz : **ESC , :wq, ENTER**

Artık diğer developer'ın yaptığı değişiklikler de sizin localinizde. Şimdi push dediğinizde kendi değişikliklerinizi de sunucuya gönderebilirsiniz. `git log` komutunu çalıştırınca neler olduğunu daha iyi anlayacaksınız. (Lütfen aşağıdan yukarıya doğru okuyunuz.)

![enter image description here][12]

Ben "Eklemeler yapıldı." şeklinde bir commit yapmışım. Tam sunucuya gönderecekken Özgür benden önce bir commit (deneme dosyası eklendi) push etmiş. Dolayısıyla ben önce Özgür'ün commitini localime aldım, merge ettim, daha sonra kendi commit'imi sunucuya gönderdim. Böylece ikimizin de yaptığı değişiklikler sunucuya gönderilmiş oldu. Özgür ne değişiklik yapmış bir bakalım :

![enter image description here][13]

Özgür `deneme.cpp` adında yeni bir dosya oluşturmuş (New file mode). `ls` komutu çalıştırınca bu dosyanın da bana geldiğini görebilirsiniz.

Bu şekilde yüzlerce, binlerce developer birlikte çalışabilirsiniz. Siz uygulamanın bir modülü üzerinde çalışırken, bir başkası farklı bir modülü üzerinde çalışabilir ve kolayca diğer developerların değişikliklerini kendi bilgisayarınıza alabilirsiniz. Bu durumda sunucuda her zaman projenin en güncel hali bulunmuş oluyor. Ancak diğer developerlar sizinle aynı dosya üzerinde çalışıyorsa ne olacak? Sizin eklediğiniz bir satırı bir başkası silerse ne olacak? Hanginizinki kullanılacak? Bu soruları bir sonraki başlıkta cevaplayacağım. 


[10]: http://i.imgur.com/bbkQQxy.png
[11]: http://i.imgur.com/fw3buIN.png
[12]: http://i.imgur.com/JZlgbO1.png
[13]: http://i.imgur.com/Qq0hes4.png
