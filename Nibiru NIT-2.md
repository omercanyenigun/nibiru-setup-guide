![alt text](https://i.hizliresim.com/7fb07pp.jpeg)

# Bilinmesi Gerekenler

- **Testnete katılacak olduğunuz cüzdan ile gleam görevlerini yapmış olmanız gerek. Eğer yapmamışsanız: https://gleam.io/yW6Ho/nibiru-incentivized-testnet-registration**

- **NIT-2 Görev ve Puanlama hakkında bilgi: https://github.com/omercanyenigun/nibiru-setup-guide/blob/main/NIT-2%20G%C3%B6revleri.md**


# Yönetişim (Governance) Görevleri

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

# Akıllı Sözleşme (Smart Contract) Görevleri

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

Eğer sunucuda node kurulu değilse cüzdanınızı import edin. Kurulu cüzdanda yapıyorsanız bi alttaki kodlardan devam edin.

![alt text](https://i.hizliresim.com/2d7kq32.png)

```
nibid keys add wallet --recover
```

```
cd $HOME/nibidcontract
```

```
nibid tx wasm store $HOME/nibidcontract/cw1_whitelist.wasm --from <cüzdanisminiz> --gas=2000000 --fees=50000unibi
```

![alt text](https://i.hizliresim.com/kjy5wie.png)

y'ye basıp devam edin çıkan çıktıda txhash ve code_id'yi bir yere kaydedin.

![alt text](https://i.hizliresim.com/gridqym.png)













