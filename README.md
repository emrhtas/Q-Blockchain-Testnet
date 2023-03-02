# Q-Blockchain-Testnet



## 🟢 Ödül Programı

 * [Medium Detay](https://medium.com/q-blockchain/q-blockchain-validator-onboarding-program-part-1-validator-incentivized-testnet-567ef6e4002e)
 * [Ödül Kayıt Linki](https://itn.qdev.li/)
 
Matemask Q ağını Ekleyin.

* Ağ Adı : Q Test Ağı
* Yeni RPC URL adresi : https://rpc.qtestnet.org
* Zincir Kimliği : 35443
* Para Birimi Sembolü : Q
* Blok Gezgini URL Adresi : https://explorer.qtestnet.org
<br>
Kayıt sonrası size Örnek  : TN-Hercules-47ds34 Böyle bir isim verecek  
<br>cd testnet-public-tools/testnet-validator/  
 
dizininde bulunan  docker-compose.yaml  dosyasındaki adınızı değiştireceksiniz. Stats explorer adresinde aşağıdaki gibi görünecek adresiniz

<br>

![image](https://user-images.githubusercontent.com/101635385/206707554-02792278-1508-40fc-a3d8-12a904561a83.png)

 
<br>ÖNCE NODE KURUYORSUNUZ AŞAĞIDAKİ GİBİ DAHA SONRA KAYIT OLUYORSUNUZ. DAHA SONRA ÜSTTEKİ İŞLEMLERİ YAPIYOR VE İSMİ DEĞİŞTİRİYORSUNUZ DEĞİŞTİRDİKTEN SONRA NODEYİ DURDURUP TEKRAR BAŞLATMANIZ GEREKİYOR.
 

## 🟢 Gerekli notlar:
### Explorer:
 * [Explorer](https://explorer.qtestnet.org/)
### Faucet:
 * [FAUCET](https://faucet.qtestnet.org/)
 

 * Testnet Teşvikli olduğunu söylüyorlar. Sitesinden inceleyebilirsiniz. 
 * 1- kurulum cd testnet-public-tools/testnet-validator/ dizininde yapılması gerekiyor. 
 * 2- Kurulum cd  testnet-public-tools/omnibridge-oracle/ dizininde yapılması gerekiyor.
 * 3- Kurulum cd  testnet-public-tools/omnibridge-ui/  dizininde yapılması gerekiyor.
 * 4- Kurulum cd  testnet-public-tools/omnibridge-alm/  dizininde yapılması gerekiyor.
 
 * 4 parti kurulumdan oluşuyor Önce Validatör kuruyoruz daha sonra Oracle kurulumu yapıyoruz.
 
 * `https://rpc.ankr.com/eth_rinkeby` Rinkeby Testnet RPC ekleyeceğiz


 ## 🟢 Kurulumlar:
 ## 2-3-4. kurulumlar Testnetten Muaf Tutuldu kurup kurmamak size kalmış.

 * 1 testnet-public-tools/testnet-validator/ <br><br>
 * 2 testnet-public-tools/omnibridge-oracle  <br>
 * 3 testnet-public-tools/omnibridge-ui <br>
 * 4 testnet-public-tools/omnibridge-alm <br>



 
 ## 🟢 Sistemi Gereksinimleri

* Ekip tarafından önerilen  <br> 4 CPU <br> 8 GB RAM <br> 250 GB Disk Alanı
 


## 🟢 Sistemi Güncelleme
```shell
sudo apt update && sudo apt upgrade -y
```

## 🟢 Gerekli Kütüphanelerin Kurulması
```shell
apt install ca-certificates curl gnupg lsb-release git htop
```

## 🟢 Docker Kurulumu
```shell

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io
docker version
```


## 🟢 Docker Compose Yüklenmesi
```shell
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## 🟢 1. KURULUM Q Network Dosyalarının İndirilmesi ve Kurulumu

## Q Network Dosyalarını İndiriyoruz
```
screen -S qnetwork
git clone https://gitlab.com/q-dev/testnet-public-tools
```

## 🟢 keystore Klasörü ve pwd.txt Dosyası Oluşturulması 
Aşağıdaki komutla `testnet-validator` dosyası içerisinde `keystore` klasörü ve onun içerisine de bize verilecek cüzdanımız için şifremizi yazacağımız `pwd.txt` dosyasını oluşturup bu doyasnın içerisine giriyoruz. Şifremizi yazıp `ctrl x y enter` ile kaydedip çıkıyoruz.

```
cd testnet-public-tools/testnet-validator/
mkdir keystore
echo ŞİFRENİZİ-YAZIN > keystore/pwd.txt
```

## Cüzdan Oluşturma
```
cd
cd testnet-public-tools/testnet-validator/
docker-compose run --rm --entrypoint "geth account new --datadir=/data --password=/data/keystore/pwd.txt" testnet-validator-node

```

Yukarıdaki kodu girdikten sonra aşağıdaki gibi bir çıktı almanız gerekiyor. Eğer böyle bir çıktı aldıysanız, her şey yolundadır. 
```
Your new key was generated

Public address of the key:   0xb3FF24F818b0ff6Cc50de951bcB8f86b522aa  -  SİZE BÖYLE BİR MATEMASK ADRESİ VERECEK
Path of the secret key file: /data/keystore/UTC--2021-01-18T11-36-28.705754426Z--b3ff24f818b0ff6cc50de951bcb8f86b52287dac

- You can share your public address with anyone. Others need it to interact with you.
- You must NEVER share the secret key with anyone! The key controls access to your funds!
- You must BACKUP your key file! Without the key, it's impossible to access account funds!
- You must REMEMBER your password! Without the password, it's impossible to decrypt the key!
```

## Kurulumu Yapılandırma

`.env` dosyası içerisine giriyoruz.<br>


```
cd
cd testnet-public-tools/testnet-validator/
cp .env.example .env
nano .env
```
Dosyada aşağıdaki yerleri dolduruyoruz.
 - `METAMASK_ADRESI` bu bölümüme yukarıda size verilen cüzdan adresini başında `0x` olmadan yazıyorsunuz.
 - `IP_ADRESI` bölümüne sunucunuzun ip adresini yazıyorsunuz.
 - Son olarak `ctrl x y enter` tuşlayarak dosyayı kaydediyoruz.

<br>

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/0aa05732-9d25-4a52-a4e1-aae61c6c659c.png" width="650">

## Matemask Cüzdan aktarma

testnet-public-tools/testnet-validator/keystore/ Dizininde UTC ile başlayan bir json dosyası göreceksiniz bunu bilgisayarınıza indirin. 
<br> Daha sonra Matemask cüzdanınızı açın ve içine json olarak import edin
<br> daha Sonra bu cüzdanın private keyini alın.
<br> Aşağıdaki 2 . Kurulum `omnibridge-oracle`  Bölümünde bu private key lazım olacak.

<img src="https://raw.githubusercontent.com/herculessx/Q-Network-Testnet/main/utc.PNG" width="650">

## config.json Dosyasını Düzenleme
Dosya içerisine giriyoruz.
```
nano config.json
```
Aşağıdaki yerleri düzenliyoruz;
 - `METAMASK_ADRESI` bu bölümüme yukarıda size verilen cüzdan adresini başında `0x` olmadan yazıyorsunuz.
 - `SIFRE` bölümüne sifrenizi.
 - Son olarak `ctrl x y enter` tuşlayarak dosyayı kaydediyoruz.
```
 {
      "address": "METAMASK_ADRESI",
      "password": "SIFRE",<br>
      "keystoreDirectory": "/data",
      "rpc": "https://rpc.qtestnet.org"
    }
```

<br>
<img src="https://github.com/herculessx/Q-Network-Testnet/blob/main/conf.png" width="650">
<br>

## Validatore Stake Etme
Bu işlemi yapmadan önce [faucetten](https://faucet.qtestnet.org/) token istemeyi unutmayın. 
```
docker run --rm -v $PWD:/data -v $PWD/config.json:/build/config.json qblockchain/js-interface:testnet validators.js
```

## Validatorumuzu https://stats.qtestnet.org Adresine Ekleme
```
nano docker-compose.yaml
```
Dosya içerisinde aşağodaki bölümü düzenliyoruz;
* `VALIDATOR_ADINIZ` bu bölüme validator adımızı yazıyoruz.

Alttaki kodu komple kopyalayın ve docker-compose.yaml dosyasındaki ile değiştirin burada sadece VALİDATÖR-İSMİNİZ yazan kısmı değiştirip kaydedin. ctrl + x Yes diyip kaydedin

```
version: "3"

services:
  testnet-validator-node:
    image: $QCLIENT_IMAGE
    entrypoint: [
      "geth",
      "--testnet",
      "--datadir=/data",
      "--syncmode=full",
      "--ethstats=VALIDATOR_STATS_ID:qstats-testnet@stats.qtestnet.org",
      "--whitelist=3699041=0xabbe19ba455511260381aaa7aa606b2fec2de762b9591433bbb379894aba55c1",
      "--bootnodes=$BOOTNODE1_ADDR,$BOOTNODE2_ADDR,$BOOTNODE3_ADDR",
      "--verbosity=3",
      "--nat=extip:$IP",
      "--port=$EXT_PORT",
      "--unlock=$ADDRESS",
      "--password=/data/keystore/pwd.txt",
      "--mine",
      "--miner.threads=1",
      "--miner.gasprice=1",
      "--rpc.allow-unprotected-txs"
    ]
    volumes:
      - ./keystore:/data/keystore
      - ./additional:/data/additional
      - testnet-validator-node-data:/data
    ports:
      - $EXT_PORT:$EXT_PORT
      - $EXT_PORT:$EXT_PORT/udp
    restart: unless-stopped

volumes:
  testnet-validator-node-data:
```

## Node'u Başlatma
```
docker-compose up -d
```

## Loglara Bakma
```
docker-compose logs -f --tail "100"
```
<br>CTRL + A + D ile ana ekrana dönelim 
