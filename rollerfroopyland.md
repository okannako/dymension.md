- Ödüllü testnet için Roller çalıştırma işlemini nasıl yapacağımıza dair yeni kılavuzlar yayınladı. O kılavuzlardan yararlanarak tek bir yerde, baştan sona işlemleri nasıl yapacağınıza dair bütün adımları bu kılavuz ve video ile kolay hale getirmeye çalıştım. Mutlaka VİDEO ile birlikte işlemleri gerçekleştirin. Kolay gelsin.

## Tavsiye Edilen Sistem Gereksinimleri
- CPU: Dual Core
- RAM: 16GB+
- SSD: 500GB+
- İşletim Sistemi: Ubuntu 22.04LTS

## Yükleme ve Çalıştırma

- Tmux ekranı açtıktan sonra ilk olarak aşağıdaki kod ile Roller'ı yükleyip daha sonra versiyon kontrolü yapıyoruz.
```cd
 sudo apt install tmux
 tmux new -s dymroller
```
```
curl -L https://dymensionxyz.github.io/roller/install.sh | bash
```
- ```roller version``` kodu ile versiyon kontrolü yapıyoruz.

- Şimdi init işlemi yapacağız yani oluşturacağımız Rollap ile ilgili ayarmalar gerçekleştireceğiz. İlk Olarak aşağıdaki kodu girince bize seçim için bir ekran çıkartacak. 
```
roller config init --interactive
```
- Kodu girdikten sonra yapacağınız seçimleri aşağıya sırayla bırakıyorum.
  - Froopyland
  - EVM
  - Burada kendinize göre bir ID girecekseniz. Örnek olarak ```berlin_9191-2``` gibii. İsim rastgele olabilir ancak düzen bu şekilde olmalı yoksa hata verir.
  - Bu adımda token için bir isim belirliyorsunuz. Örnek olarak >>> BTC, PEPE, DYM...
  - Token Supply belirliyoruz. Enterlarsanız otomatik 1B olur sayı.
  - Celestia/Avail
  - EVM

- Bize verdiği adresler cüzdan adreslerimiz ve buna Discord'dan test tokenı almamız lazım >> https://discord.gg/dymension. Eğer Avail seçtiyseniz onun coininni kendi Discordundan almalısınız. 
```
Sequencer <network> | Address used to publish state updates to the Dymension Hub
Relayer   <network> | Address that handles the relaying of IBC packets
DA        <network> | Address used to publish data on-chain to the DA network
```

- Test tokenlarını ilk iki adres için froopyland-faucetten Celestia için celestia-faucetten Avail için kendi discordundan alıyorsunuz. Alırken ```$request dym15a....``` ve ```$request celestia1``` şeklinde yazıp istemelisiniz. Bir süre sonra ```$balance cüzdanadresi``` yazarak token gelip gelmediğini kontrol edebilirsiniz.

- Roller kayıt için şu kodu girmeniz yeterli ```roller register``` ve size şuna benzer bir çıktı vermeli ```💈 Rollapp '<rollapp-id>' has been successfully registered on the hub.```

- Ve Artık son adım olan Roller çalıştırmaya geçebiliriz. Şu kodla ```roller run``` Roller çalıştıktan sonra aşağıdaki gibi bir çıktılar vermeli. İlk resim başlattığınız andaki durum ikinci resim ise belirli bir süre sonunda kanal açıldıktan sonraki çıktı. İkinci resimdeki gibi bir çıktı vermeden işlemlere devam etmeyin.
![aaaaaa](https://github.com/okannako/dymension.md/assets/73176377/cfa18c15-4fae-46dd-9542-729a97221013)

- Tabloda bulunan değerlerin ne demek olduğunu aşağıda bulabilirsiniz
```
Height: latest RollApp block height
Hub: latest RollApp block height that was published to the Dymension Hub
Port 8545: EVM RPC provides a RPC gateway for publishing EVM smart contracts
Port 26657: Node RPC provides a RPC gateway for requests to the node
Port 1317: Rest end-point provides a REST gateway for requests to the node
Log file path: is the PATH to the RollApp logs
```

## IBC Transfer

- Aşağıdaki kodla faucet aldığımız adrese token göndereceğiz. Aşağıdaki kodda <base-denom>'u tamamen silip token için verdiğimiz ismin başuna u ekleyerek yerine yazıyoruz. Bu işlemin gerçekleşmesi 15 dakikayı bulabilmektedir.
```
rollapp_evm tx ibc-transfer transfer transfer channel-0 dym1g8sf7w4cz5gtupa6y62h3q6a4gjv37pgefnpt5 5000000000000000000000000<base-denom> --from rollapp_sequencer --keyring-backend test --home ~/.roller/rollapp --broadcast-mode block
```
- Belirli bir süre sonra Discord'da froopyland-faucet kanalından aşağıdaki kodla tokenınızın adreste olup olmadığına bakabiliyorsunuz ve varsa talep edebiliyorsunuz. İlk kod adreste token olup olmadığını sorgulamayı gerçekleştiriyor. İkinci kod ike adresinize talep edebiliyorsunuz. <rollapp-id>'yi silip kendi belirlediğimiz id'yi giriyoruz. 
 - ```$balances dym1g8sf7w4cz5gtupa6y62h3q6a4gjv37pgefnpt5 <rollapp-id>```
 - ```$request <user-address> <rollapp-id>```

- RollApp Form >>> https://dymension.typeform.com/RollAppListing
- Explorer >>> https://explorer.silknodes.io/dymension

## KEY Yedeklemek

- Arkadaşlar geldik en önemli işleme, bu işlem ile oluşan keylerimizin yedeğini alıp bilgisayar vs. bir yerde kesinlikle saklıyoruz. İlk kod keylerimizi gösterir, 2 3 ve 4. kodlarda yedeği almamızı sağlıyor. Ayrıca Winscp ile bağlanıo .roller klasörünü de taşıma ya da çökmelere önlem için yedeklemeniz iyi olacaktır. ÖNEMLİ!!
- ```roller keys list```
- ```roller keys export hub_sequencer```
- ```roller keys export rollapp_sequencer```
- ```roller keys export my_celes_key```

- Fork ve Yıldız için Teşekkürler.
