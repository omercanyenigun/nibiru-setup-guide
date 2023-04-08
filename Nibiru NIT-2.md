![alt text](https://i.hizliresim.com/7fb07pp.jpeg)

# Bilinmesi Gerekenler

- **Testnete katılacak olduğunuz cüzdan ile gleam görevlerini yapmış olmanız gerek. Eğer yapmamışsanız: https://gleam.io/yW6Ho/nibiru-incentivized-testnet-registration**

- **NIT-2 Görev ve Puanlama hakkında bilgi: https://github.com/omercanyenigun/nibiru-setup-guide/blob/main/NIT-2%20G%C3%B6revleri.md**


# Yönetişim (Governance) Görevi

Proposallara oylama yapmak için explorer üzerinden (https://nibiru.explorers.guru/proposals) active lan proposalların ID numaralarını girerek oy verebilirsiniz. Kodlarda değiştirilecek olan yerler ID numaraları ve cüzdan isimleri. İsterseniz Keplr wallet uygulamasını (https://explorer.kjnodes.com/nibiru-testnet/gov) sitesine bağlayarak oy verebilirsiniz. 

![alt text](https://i.hizliresim.com/sskpd0l.png)

- **Evet oyu**

```
nibid tx gov vote <IDnumarası> yes --from <cüzdanismi> --chain-id nibiru-itn-1 --gas-prices 0.1unibi --gas-adjustment 1.5 --gas auto -y 
```

- **Hayır oyu**

```
nibid tx gov vote <IDnumarası> no --from <cüzdanismi> --chain-id nibiru-itn-1 --gas-prices 0.1unibi --gas-adjustment 1.5 --gas auto -y 
```

- **Çekimser**

```
nibid tx gov vote <IDnumarası> abstain --from <cüzdanismi> --chain-id nibiru-itn-1 --gas-prices 0.1unibi --gas-adjustment 1.5 --gas auto -y 
```

# Akıllı Sözleşme (Smart Contract) Görevi

Buradaki işlemleri nibiru node kurulu olan sunucuda yapabileceğiniz gibi kurulu olmayan sunucuda da yapabilirsiniz. Eğer sunucuda nibiru node kurulu değilse cüzdanınızı (gleam sitesine girdiğiniz cüzdan) import edin.

```
curl -s https://get.nibiru.fi/! | bash
```
```
nibid config node https://rpc.itn-1.nibiru.fi:443
nibid config chain-id nibiru-itn-1
nibid config broadcast-mode block
nibid config keyring-backend file
```

```
git clone https://github.com/NibiruChain/cw-nibiru
```


Eğer sunucuda glaam'e verdiğiniz cüzdan yoksa cüzdanınızı import edin. Kurulu cüzdanda yapıyorsanız bi alttaki kodlardan devam edin. (nibid keys add wallet --recover kodunu atlayın)

```
nibid keys add wallet --recover
```

![alt text](https://i.hizliresim.com/m4x5xg7.png)


Koddaki cüzdanadınız yerini değiştirin.

```
nibid tx wasm store $HOME/cw-nibiru/artifacts-cw-plus/cw20_base.wasm --from cüzdanadınız --gas-adjustment 1.5 --gas auto --fees 90000unibi  -y
```

![alt text](https://i.hizliresim.com/knrdd23.png)

Resimdeki gibi code_id'nizi ve txhash değerinizi kaydedin.

Eğer code_id’nizi bulmak isterseniz txhashdeğeriniz yerine txhash'inizi girin

```
nibid q tx txhashdeğeriniz | grep raw_log
```
![alt text](https://i.hizliresim.com/r9odcpc.png)

code_id kontrolü (code_idniz olan yere id numaranızı girin)

```
id=code_idniz
```
```
nibid query wasm code-info $id
```

![alt text](https://i.hizliresim.com/cr3rq2t.png)


# ExecuteContract İşlemi

```
CONTRACT=$(nibid query wasm list-contract-by-code $id --output json | jq -r '.contracts[-1]')
```

Eğer kodu yazdığınızda jq hatası alırsanız alttaki kodu girin

```
apt  install jq
```

koddaki tokengöndereceğinizadres yerine göndermek istediğiniz adresi girin

```
TRANSFER='{"transfer":{"recipient":"tokengöndereceğinizadres","amount":"150"}}'
```
Koddaki cüzdanadınız yerini değiştirin.

```
nibid tx wasm execute $CONTRACT $TRANSFER --gas-adjustment 1.5 --gas auto --fees 6000unibi --from cüzdanadınız -y
```

![alt text](https://i.hizliresim.com/80mbr06.png)


Kontrol etmek isterseniz

```
BALANCE_QUERY='{"balance": {"address": "tokengönderdiğinizadres"}}'
```
```
nibid query wasm contract-state smart $CONTRACT "$BALANCE_QUERY" --output json
```

![alt text](https://i.hizliresim.com/8ab0jmy.png)


Eğer aşağıdaki gibi hata alırsanız, ya tekrar tekrar denemeniz yada rpc değiştirmeniz gerekir.


![alt text](https://i.hizliresim.com/jv56o4w.png)















