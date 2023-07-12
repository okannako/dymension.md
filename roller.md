- Ödüllü testnet öncesi Roller çalıştırma işlemini nasıl yapacağımıza dair yeni kılavuzlar yayınladı. O kılavuzlardan yararlanarak tek bir yerde, baştan sona işlemleri nasıl yapacağınıza dair bütün adımları bu kılavuz ve video ile kolay hale getirmeye çalıştım. Kolay gelsin.

## Tavsiye Edilen Sistem Gereksinimleri
- CPU: Dual Core
- RAM: 16GB+
- SSD: 500GB+
- İşletim Sistemi: Ubuntu 22.04LTS

- İlk olarak aşağıdaki kod ile Roller'ı yükleyip daha sonra versiyon kontrolü yapıyoruz.
```
curl -L https://github.com/dymensionxyz/roller/releases/download/v0.1.2/install.sh | bash
```
```roller version``` >> ```Roller version v0.1.2```

- Şimdi init işlemi yapacağız yani oluşturacağımız Rollap ile ilgili ayarmalar gerçekleştireceğiz. İlk Olarak aşağıdaki kodu girince bize seçim için bir ekran çıkartacak. 
```
roller config init --interactive
```
- Kodı girdikten sonra yapacağınız seçimleri aşağıya sırayla bırakıyorum.
  - Devnet
  - Burada kendinize göre bir ID girecekseniz. Örnek olarak ```berlin_9191-2``` gibii. İsim rastgele olabilir ancak düzen bu şekilde olmalı yoksa hata verir.
  - Bu adımda token için bir isim belirliyorsunuz. Örnek olarak >>> BTC, PEPE, DYM...
  - Token Supply belirliyoruz. Enterlarsanız otomatik 1B olur sayı.
  - Celestia
  - EVM

- Bize verdiği adresler cüzdan adreslerimiz ve buna Discor'dan test tokenı almamız lazım >> https://discord.gg/dymension
```
Sequencer <network> | Address used to publish state updates to the Dymension Hub
Relayer   <network> | Address that handles the relaying of IBC packets
DA        <network> | Address used to publish data on-chain to the DA network
```

- Test tokenlarını ilk iki adres için devnet-faucetten Celestia için celestia-faucetten alıyorsunuz. Alırken ```$request dym15a....``` ve ```$request celestia1``` şeklinde yazıp istemelisiniz. Bir süre sonra ```$balance  cüzdanadresi``` yazarak token gelip gelmediğini kontrol edebilirsiniz.

- Roller kayıt için şu kodu girmeniz yeterli ```roller register``` ve size şuna benzer bir çıktı vermeli ```💈 Rollapp '<rollapp-id>' has been successfully registered on the hub.```

- Ve Artık son adım olan Roller çalıştırmaya geçebiliriz. Şu kodla ```roller run``` Roller çalıştıktan sonra aşağıdaki gibi bir çıktı vermeli.

