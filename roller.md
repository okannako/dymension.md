
- Ödüllü testnet öncesi Roller çalıştırma işlemini nasıl yapacağımıza dair yeni kılavuzlar yayınladı. O kılavuzlardan yararlanarak tek bir yerde, baştan sona işlemleri nasıl yapacağınıza dair bütün adımları bu kılavuz ve video ile kolay hale getirmeye çalıştım. Kolay gelsin.

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
curl -L https://github.com/dymensionxyz/roller/releases/download/v0.1.2/install.sh | bash
```
```roller version``` >> ```Roller version v0.1.2```

- Şimdi init işlemi yapacağız yani oluşturacağımız Rollap ile ilgili ayarmalar gerçekleştireceğiz. İlk Olarak aşağıdaki kodu girince bize seçim için bir ekran çıkartacak. 
```
roller config init --interactive
```
- Kodu girdikten sonra yapacağınız seçimleri aşağıya sırayla bırakıyorum.
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

- Test tokenlarını ilk iki adres için devnet-faucetten Celestia için celestia-faucetten alıyorsunuz. Alırken ```$request dym15a....``` ve ```$request celestia1``` şeklinde yazıp istemelisiniz. Bir süre sonra ```$balance cüzdanadresi``` yazarak token gelip gelmediğini kontrol edebilirsiniz.

- Roller kayıt için şu kodu girmeniz yeterli ```roller register``` ve size şuna benzer bir çıktı vermeli ```💈 Rollapp '<rollapp-id>' has been successfully registered on the hub.```

- Ve Artık son adım olan Roller çalıştırmaya geçebiliriz. Şu kodla ```roller run``` Roller çalıştıktan sonra aşağıdaki gibi bir çıktı vermeli.

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
rollapp_evm tx ibc-transfer transfer transfer channel-0 dym12ad4lux36lta7d75v2w6je2y386y9s5xp658pz 1000000000000000000<base-denom> --from rollapp_sequencer --keyring-backend test --home ~/.roller/rollapp --broadcast-mode block
```
- Belirli bir süre sonra Discord'da devnet-faucet kanalından aşağıdaki kodla tokenınızın adreste olup olmadığına bakabiliyorsunuz ve varsa talep edebiliyorsunuz. İlk kod adreste token olup olmadığını sorgulamayı gerçekleştiriyor. İkinci kod ike adresinize talep edebiliyorsunuz. <rollapp-id>'yi silip kendi belirlediğimiz id'yi giriyoruz. 
 - ```$balances dym12ad4lux36lta7d75v2w6je2y386y9s5xp658pz <rollapp-id>```
 - ```$request <user-address> <rollapp-id>```

## KEY Yedeklemek

- Arkadaşlar geldik en önemli işleme, bu işlem ile oluşan keylerimizin yedeğini alıp bilgisayar vs. bir yerde kesinlikle saklıyoruz. İlk kod keylerimizi gösterir, 2 3 ve 4. kodlarda yedeği almamızı sağlıyor. ÖNEMLİ!!
 ```roller keys list```
 ```roller keys export hub_sequencer```
 ```roller keys export rollapp_sequencer```
 ```roller keys export my_celes_key```

NOT: Develop işlemleride var onları yapmayacağım şimdilik ama uğraşmak isterseniz linkini aşağıya bırakıyorum. Kolay gelsin.
 - https://docs.dymension.xyz/build/quick-start/evm/connect

