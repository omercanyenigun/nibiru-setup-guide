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
PEERS="a1b96d1437fb82d3d77823ecbd565c6268f06e34@nibiru-testnet.nodejumper.io:27656,ac163da500a9a1654f5bf74179e273e2fb212a75@65.108.238.147:27656,abab2c6f45fa865dc61b2757e21c5d2244e5bacb@213.202.218.55:26656,fe17db7c9a5f8478a2d6a39dbf77c4dc2d6d7232@5.75.189.135:26656,7e75b2249d088a4dfc3b33f386c316cb47366d2b@195.3.221.48:11656,6db03cd0732b5120c291065694bafaf9c76baf4c@213.202.247.87:26656,b02f28e0675743b077186b363386f10845c9e122@194.233.74.249:26656,c1b40d056e4260a9fa9d1142af1adbeec5039599@142.132.202.50:46656,ea44a000ee4df9d722a90fdf41b3990e738bdda0@65.109.235.95:26656,9f20e1096408d3fa15fafea8fe282ba310d35a53@38.242.159.148:27656,e08089921baf39382920a4028db9e5eebd82f3d7@142.132.199.236:21656,dfdfca675e009578b775d7febace9d15d97c3755@207.180.224.21:26656,bab9f78f1c0ccd5b4d9db13a112dcf45c60e4df1@130.193.68.154:26656,d327bb6b997a32aaa7dae5673e9a9cbad487ad09@104.156.250.70:26656,4f1af4f62f76c095d844384a3dfa1ad76ad5c078@65.108.206.118:60656,9d901d286eda108828250c0a9e65fef72ee293cd@129.146.80.192:26656,ee76ff1711d63ab37efa77cb669e21643b0f2609@65.109.39.103:26656,f2e99f5a68adfb08c139944a193e2e3a4864b038@167.235.132.74:26656,c8907a13b012e7a937cfe7d624b0fbe7ef3508b2@194.163.160.155:26656,53db2490d7f6601a55aa59e98e4d6cfd5d8a929c@51.159.187.67:36656,30e14f66fc44a55a51f36693afd754283c668953@65.108.200.60:11656,fa5c730d842aff05c3761d9c1b06107340ac7651@65.108.232.238:11656,f01ad3a75b255226499df9183ac2ebc0a40a9e05@46.4.53.207:33656,81a8383eefae628ae4bc400d52d49adfb11cb76a@65.108.108.52:11656,1c548375968f0abfac3733cae9f592468c988bf9@46.4.53.209:33656,cd44f2d2fc1ded3a63c64f46ed67f783c2d93d57@144.76.223.24:36656,b03d1ce3e97984a8b8a63a7a6ec6c5d196d81436@46.4.53.208:33656,e74f1204d65d0264547e2c2d917c23c39fcff774@95.217.107.96:36656,b88642986618adc6d47ed32db1a5f2e086da18b8@132.145.209.220:26656,79e2bfc202e39ba2a168becc4c75cb6a56803e38@135.181.57.104:11656,22d5b4919850ad71ad0a1bf7979c7dba53960689@192.9.134.157:27656,3fbc70ee59230284f834931cc8edf1e16f9659e3@65.108.43.58:27667,a3a344c1732c507f40931778225f919004392e94@52.204.188.236:26656,d3e7948a5ba3f55264f1260c1d102924616b6711@5.180.186.27:26656,98032241ea61ca6ac066b8fa508baace6678a7a3@190.2.155.67:31656,5f3394bae3791bcb71364df80f99f22bd33cc2c0@95.216.7.169:60556,96c04b7aab96ee38eabdb909d64c16dc3d419911@154.12.241.215:29656,a08e5b25443d038b08230177456ee23196509dd5@65.109.92.79:12656,10382838df100f7817eb9c86c5da67160eefe4fc@95.216.100.241:30656,62d93ddd046e8092c3717117484ed680cbacbf0d@139.59.239.43:26656,f29c808ff578c7f3a3746b9b0b3e0504b3ee2315@65.108.216.139:26656,1c471515138388224c40825fb056f6f34650bf8c@188.233.19.230:26656,ff923b3fe54b99d4a02840421459c8e5cce1de2d@89.58.34.200:26656,be58621ecdf7dae1ff6fa5123793ddbc794427b1@65.21.248.137:26656,aad0d897a82880e36bb909091c5878607446ab41@138.201.204.5:35656,595a8f93897710cacc3173c9ae4d0bafda5b3879@141.94.73.93:36656,39cf8864b1f1655a007ece6c579b290a9132082b@65.109.143.6:26656,5ebe46c59e50eb3eefda23f8400aed4ce1c56ad1@194.195.87.49:26656"
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


- **İsteğe bağlı snap kullanabilirsiniz (540,226k)**

```
sudo systemctl stop nibid

cp $HOME/.nibid/data/priv_validator_state.json $HOME/.nibid/priv_validator_state.json.backup 

nibid tendermint unsafe-reset-all --home $HOME/.nibid --keep-addr-book 
curl https://snapshots2-testnet.nodejumper.io/nibiru-testnet/nibiru-itn-1_2023-03-02.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.nibid

mv $HOME/.nibid/priv_validator_state.json.backup $HOME/.nibid/data/priv_validator_state.json 

sudo systemctl start nibid
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

- **Discord** - **https://discord.gg/nibiru**

$request <cüzdan-adresiniz>

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



















