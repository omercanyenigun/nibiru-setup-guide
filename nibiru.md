# Nibiru-Setup-Guide (Cosmovisor)

![alt text](https://i.hizliresim.com/ary8n1w.png)

**Minimum Sistem Gereksinimleri**

- **4 CPU**
- **8GB RAM**
- **160GB DISK**
- **Ubuntu 20.04+**

- **Gerekli Güncellemeler ve Bağlılıklae**

```
sudo apt update && sudo apt upgrade -y && sudo apt install curl tar wget clang pkg-config libssl-dev jq build-essential bsdmainutils git make ncdu gcc git jq chrony liblz4-tool -y
```

- **Go Kurulum**

```
ver="1.19.5"
cd $HOME
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
source ~/.bash_profile
```

- **Go Versiyon Kontrol**

```
go version
```
![alt text](https://i.hizliresim.com/chw0332.png)

- **Binary Yüklemesi**

```
cd $HOME
rm -rf nibiru
git clone https://github.com/NibiruChain/nibiru.git
cd nibiru
git checkout v0.19.2
make build
```

- **Cosmovisor**

```
mkdir -p $HOME/.nibid/cosmovisor/genesis/bin
mv build/nibid $HOME/.nibid/cosmovisor/genesis/bin/
rm -rf build
```
```
sudo ln -s $HOME/.nibid/cosmovisor/genesis $HOME/.nibid/cosmovisor/current
sudo ln -s $HOME/.nibid/cosmovisor/current/bin/nibid /usr/local/bin/nibid
```

- **nibid'ün başarılı yüklendiğinin kontrolü**

```
nibid version
```
![alt text](https://i.hizliresim.com/d688ybz.png)

- **Cosmovisor Kurulumu**

```
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@v1.4.0
```

- **Yapılandırma**

```
nibid config chain-id nibiru-itn-1
nibid config keyring-backend test
```

- **Node Kurulumu**

#moniker-isminiz olan yeri değiştirin**
  
```
nibid init <moniker-isminiz> --chain-id nibiru-itn-1
```

- **Genesis**

```
wget https://raw.githubusercontent.com/omercanyenigun/nibiru-setup-guide/main/genesis.json -O $HOME/.nibid/config/genesis.json
```

- **Seeds ve Peers'i Yapılandırma**

```
SEEDS=""
PEERS="a1b96d1437fb82d3d77823ecbd565c6268f06e34@nibiru-testnet.nodejumper.io:27656,39cf8864b1f1655a007ece6c579b290a9132082b@65.109.143.6:26656,19f6588df6e489a3e512ebac805c5250cdc9fbb7@84.46.249.14:26656,5808c7e3cb15029cdbc9f0fb88116d2cc54ae0c1@84.46.254.241:26656,250b70b8282913d9914645c13fbdc03ae8fb89ab@194.163.130.5:26656,f545d387c8b590a0a3f07116cdd78ad08fc982e8@130.185.119.230:29656,4a73ca5f1acd581fd58f7f0147afbc4966a42ef8@84.46.252.90:26656,091ef5d449922e6de2b42039505bbd1c06a3cdc6@194.163.139.34:26656,381a034beb28a3af011526f28ac20ed08562e852@89.117.59.184:26656,65a213efcad697afb5a1303c7fe5be4168d9520c@43.154.103.36:26656,79e2bfc202e39ba2a168becc4c75cb6a56803e38@135.181.57.104:11656,8e471a078b929944d3812c44e7babe06fb32b527@178.18.249.99:26656,aacb1372d58db9bc26e39dd9e2507168df757c4a@38.242.243.75:26656,14f014b411bc72b8036c452ea5ba4e1ab7e51037@149.102.141.2:26656,f4a6bcbd4af5cfd82ee3a40c54800176e33e9477@31.220.79.15:26656,4a70de4fffde46382e70250c06f744570ce72ef9@138.201.124.93:26656,02c87754ba959dfc3ba3c4251273a9dd83e2dabb@46.42.19.179:16656,f8ddd8555ce6837fec0b64e28daa80851bd98723@148.251.43.226:21656,958281e2c828ab54c5c828557becbdad3f346ffb@65.109.87.135:35656,4ae091976ef83403cbbb55345a1af0a06f3ef524@144.76.101.41:26656,4a7065cb42272653779f41e1a9e63911743e8185@31.220.85.198:26656,2e0b94efd4bc1f96efe1aa5af347d20fea446e6e@185.48.24.222:26656,4ae7eeab8b1ec28e9a71365984dbc7fbfbefbdfe@89.163.146.199:26656,c83d16ddab9e16f61e553583f1589b9d24b7e6ac@31.220.87.238:26656,fbc4a557e0b55d2960571e3119e727bf029be699@135.181.101.33:26656,7e791abaa171405b699f7a70faed4462212c9f5b@65.21.138.123:29656,038a983cbc48be2a9ee397268b77aeb94d6ffe4c@167.86.70.119:26656,05413aea0a230e4930fc874f82617ea562c250f9@65.109.90.171:27656,06092c9a8d68640c189290abd7ee5da669865bad@31.220.90.83:26656,1eceb9c1dde5b66693f48eb0830bc8781deee3f3@161.35.19.181:26656,d0ce7b356e76298ea59aeb78397e9d84f0ed2480@31.220.88.180:26656,0cbe6d28190e5fee5f41071a622861e378421d16@161.35.17.234:03656,072975554bef679c2fa798e0e29b7606c2c20073@38.242.248.93:26656,91ad1995b05111c8f9c43cdc7f801bd202de082d@62.171.172.94:26656,0f8ea9f1dacc680e7074e8019bae16b1e8979977@89.117.58.243:26656,d8653d56d8914e5a26d7ff2f2f930dc44d593e1e@38.242.232.142:26656,eef9734e501dcac0988585e2fc56d133653b1554@185.218.124.169:11656,563b3993420bcbb7226ac1f50ce6cbf9497de1c8@66.94.101.5:26656,2ea0ad76f4c34ee9616642afd52f571248b734b1@37.27.5.51:26656,ce3b71fc75fc5085e4a6234ce4de570113e1dca4@89.117.59.7:26656,d39e7451f84c3918860954f66ce473cca70ab70e@209.250.242.119:26656,13cc216c7c2c29783fae084062f10c68f2999d83@91.229.245.201:26656,4667ea254567c150b310ac41276ef92b42b45641@89.117.59.35:26656,d26e9d2a81ce80328d3a9aeabb0820fbc343b5f4@161.97.170.91:26656,638c4ae39f363743773e97bd926875c357fe81ee@38.242.247.170:26656,ad44af0e6a86f627583d5294d3a242dc2be733da@65.109.132.189:26656,224c85918ea98d62daab63ba9eceab195b676760@144.91.71.1:26656,f8fd91b8f153279ee4ea861f4e3d5559b3efdcab@31.220.88.156:26656,c18ceb1e443b06a4ecf7aa6c92b9c143a1e94648@65.108.110.23:39656,d5f7d7ba04a7b43396c71a5fa63ff132acf59bf6@164.90.228.2:12656"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$PEERS'"|' $HOME/.nibid/config/config.toml
```

- **Pruning (isteğe bağlı)**

```
PRUNING="custom"
PRUNING_KEEP_RECENT="100"
PRUNING_INTERVAL="19"

sed -i -e "s/^pruning *=.*/pruning = \"$PRUNING\"/" $HOME/.nibid/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \
\"$PRUNING_KEEP_RECENT\"/" $HOME/.nibid/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \
\"$PRUNING_INTERVAL\"/" $HOME/.nibid/config/app.toml
```

- **Servis Dosyası Oluşturma**

```
sudo tee /etc/systemd/system/nibid.service > /dev/null << EOF
[Unit]
Description=nibiru-testnet node service
After=network-online.target

[Service]
User=$USER
ExecStart=$(which cosmovisor) run start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.nibid"
Environment="DAEMON_NAME=nibid"
Environment="UNSAFE_SKIP_BACKUP=true"
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:$HOME/.nibid/cosmovisor/current/bin"

[Install]
WantedBy=multi-user.target
EOF
```

- **Servis etkinleştirme ve Node başlatma**

```
sudo systemctl daemon-reload
sudo systemctl enable nibid
sudo systemctl restart nibid
sudo journalctl -fu nibid -o cat
```
![alt text](https://i.hizliresim.com/4590gqq.png)


- **İsteğe bağlı snap kullanabilirsiniz (1,871,692 block)**

```
sudo systemctl stop nibid

cp $HOME/.nibid/data/priv_validator_state.json $HOME/.nibid/priv_validator_state.json.backup 

nibid tendermint unsafe-reset-all --home $HOME/.nibid --keep-addr-book 
curl https://snapshots2-testnet.nodejumper.io/nibiru-testnet/nibiru-itn-1_2023-04-13.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.nibid

mv $HOME/.nibid/priv_validator_state.json.backup $HOME/.nibid/data/priv_validator_state.json 

sudo systemctl restart nibid
sudo journalctl -u nibid -f --no-hostname -o cat
```

- **Node Status (çıktı false ise nodeunuz senkronize olmuştur.)**

```
nibid status 2>&1 | jq .SyncInfo
```
![alt text](https://i.hizliresim.com/s18cuyk.png)

- **Cüzdan Oluşturma**

```
nibid keys add wallet
```

- **Önceki cüzdanı import etme (gleam'a gönderdiğiniz cüzdanı kullanın)**

```
nibid keys add wallet --recover
```
![alt text](https://i.hizliresim.com/8b40g1h.png)

- **Nibiru Discord Kanalından Faucet**

- **Discord** - **https://discord.gg/nibiruchain**

- $request <cüzdan-adresiniz>

![alt text](https://i.hizliresim.com/r6ipu40.png)


**Validatör Kurulumu**

```
nibid tx staking create-validator \
--amount=1000000unibi \
--pubkey=$(nibid tendermint show-validator) \
--moniker="moniker-adınız" \
--chain-id=nibiru-itn-1 \
--commission-rate=0.10 \
--commission-max-rate=0.20 \
--commission-max-change-rate=0.01 \
--min-self-delegation=1 \
--from=wallet \
--gas-prices=0.1unibi \
--gas-adjustment=1.5 \
--gas=auto \
-y
```

![alt text](https://i.hizliresim.com/r1ah10q.png)

# Pricefeeder

```
curl -s https://get.nibiru.fi/pricefeeder! | bash
```

```
export CHAIN_ID="nibiru-itn-1"
export GRPC_ENDPOINT="localhost:9090"
export WEBSOCKET_ENDPOINT="ws://localhost:26657/websocket"
export EXCHANGE_SYMBOLS_MAP='{ "bitfinex": { "ubtc:uusd": "tBTCUSD", "ueth:uusd": "tETHUSD", "uusdt:uusd": "tUSTUSD" }, "binance": { "ubtc:uusd": "BTCUSD", "ueth:uusd": "ETHUSD", "uusdt:uusd": "USDTUSD", "uusdc:uusd": "USDCUSD", "uatom:uusd": "ATOMUSD", "ubnb:uusd": "BNBUSD", "uavax:uusd": "AVAXUSD", "usol:uusd": "SOLUSD", "uada:uusd": "ADAUSD", "ubtc:unusd": "BTCUSD", "ueth:unusd": "ETHUSD", "uusdt:unusd": "USDTUSD", "uusdc:unusd": "USDCUSD", "uatom:unusd": "ATOMUSD", "ubnb:unusd": "BNBUSD", "uavax:unusd": "AVAXUSD", "usol:unusd": "SOLUSD", "uada:unusd": "ADAUSD" } }'
export FEEDER_MNEMONIC="mnemonic(validatör oluştururken kullandığınız)"
export VALIDATOR_ADDRESS="nibivaloper-adresiniz"
```

**Servis Dosyası Oluşturma**

```
sudo tee /etc/systemd/system/pricefeeder.service<<EOF
[Unit]
Description=Nibiru Pricefeeder
Requires=network-online.target
After=network-online.target

[Service]
Type=exec
User=$USER
ExecStart=/usr/local/bin/pricefeeder
Restart=on-failure
ExecReload=/bin/kill -HUP $MAINPID
KillSignal=SIGTERM
PermissionsStartOnly=true
LimitNOFILE=65535
Environment=CHAIN_ID='$CHAIN_ID'
Environment=GRPC_ENDPOINT='$GRPC_ENDPOINT'
Environment=WEBSOCKET_ENDPOINT='$WEBSOCKET_ENDPOINT'
Environment=EXCHANGE_SYMBOLS_MAP='$EXCHANGE_SYMBOLS_MAP'
Environment=FEEDER_MNEMONIC='$FEEDER_MNEMONIC'

[Install]
WantedBy=multi-user.target
EOF
```

![alt text](https://i.hizliresim.com/immai4k.png)

```
sudo systemctl daemon-reload && \
sudo systemctl enable pricefeeder && \
sudo systemctl start pricefeeder
```


- **Log Kontrol**

```
journalctl -fu pricefeeder
```
#Loglardaki valoper adresinin sizin validatörünüzün valoper adresi olduğuna dikkat edin.

![alt text](https://i.hizliresim.com/dje36x7.png)


#Eğer active sette değilseniz oylamalar fail olarak geçecektir.

![alt text](https://i.hizliresim.com/beoplog.png)



















