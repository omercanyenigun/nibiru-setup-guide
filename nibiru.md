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
PEERS="a1b96d1437fb82d3d77823ecbd565c6268f06e34@nibiru-testnet.nodejumper.io:27656,19f8333cbcaf4f946d20a91d9e19d5fc91899023@167.235.74.22:26656,9e9a8ffb07318c9d5237274bb32711b008b46348@91.107.233.192:26656,6f29a743ad237d435aac29b62528cea01ceb3ca9@46.4.91.90:26656,ca5805d8553b99d6e226deecd9c28a9bcb380651@161.97.163.208:26656,1c6f50dfeb2187f38e8dea2e1bae00e8b5bf6b16@161.97.102.159:26656,f9e2c35f5da87933bcc092ab9f14d45b08d3e89d@65.108.145.226:26656,1d2d3e8353043b25675040258912fb04cfc3eff9@162.55.242.81:26656,aafe706e7bb9aac7e8ec2878d775252652594b3e@78.46.97.242:26656,8e01bceecf0965c6e9f1cbce95063ae9de931ada@144.91.65.161:26656,e08089921baf39382920a4028db9e5eebd82f3d7@142.132.199.236:21656,dfdfca675e009578b775d7febace9d15d97c3755@207.180.224.21:26656,a9fd9fa7733333fa0b1f9d0868e394dd73c103da@89.116.28.98:26656,333b77ac522d86819d341cd675f962dd0ee3ae79@85.190.246.188:26656,4f1af4f62f76c095d844384a3dfa1ad76ad5c078@65.108.206.118:60656,5a58fa951f65cd2381d0f9a584fbb76fdafc476c@45.10.154.139:18656,5dd26cc6a2778cea7c0daed0a53a39c6165a790f@168.119.101.224:26656,f2e99f5a68adfb08c139944a193e2e3a4864b038@167.235.132.74:26656,bc2f0d7d7284ae91db72665d9fe154be4c2adae9@91.230.110.106:26656,a2d2ba190f32700f44e9dbe990c814f46abfc96f@81.0.221.31:26656,fc622de0732fb4ed75319c31dc83e22517a48c1c@144.91.75.58:26656,d3624259ec8322cd4b6bce5b39aaf6074f90a2ab@173.212.248.126:26656,aa166a62f6983edccd5a2619b036fe83cb4eb57e@168.119.248.238:26656,e052d62551e51b986572ea0c2e7c49ebb080b108@89.163.132.44:26656,22f1bf214da6c0c1e6c6b78bc6005ac4fc4456da@46.228.205.211:26656,cd44f2d2fc1ded3a63c64f46ed67f783c2d93d57@144.76.223.24:36656,5f794b4b6f1232e5814c66f4bd7307adcdd206cb@104.248.61.162:26656,e74f1204d65d0264547e2c2d917c23c39fcff774@95.217.107.96:36656,d12c686810ecfa63d55ac47715a542d0d73648ac@144.91.107.153:26656,79e2bfc202e39ba2a168becc4c75cb6a56803e38@135.181.57.104:11656,595a8f93897710cacc3173c9ae4d0bafda5b3879@141.94.73.93:36656,8ebed484e09f93b12be00b9f6faa55ea9b13b372@45.84.138.66:39656,81351ddd64122e553cf2c10efbd979c8c6e97529@161.97.166.105:26656,3060a899170ccb3d787d6fd840c5e8b6805f4b4d@155.133.22.140:26656,963ce4161f4d438155fa2a6c331ef067d29d2aa3@38.242.215.26:26656,5f3394bae3791bcb71364df80f99f22bd33cc2c0@95.216.7.169:60556,a141b286f68f88fa41b1e12cbf5ab079610fabd4@149.102.155.48:26656,0ce9d0e9cde24a98529a952e295c3dec712aaabf@62.141.39.131:26656,4ae091976ef83403cbbb55345a1af0a06f3ef524@144.76.101.41:26656,5b2d7ccdf924ff16c3d0e3b55c4547a71c99dc42@161.97.122.167:39656,d6121e2eb0842e03529b3a093204bebe637fa5aa@149.102.140.245:26656,455631724cc9596a3f1ca99fe6874125d050a983@38.242.225.208:26656,7b71facfb46ccd860d4d71696b3a077676a6f2b5@65.109.166.8:26656,be58621ecdf7dae1ff6fa5123793ddbc794427b1@65.21.248.137:26656,adcb0c33d521b5a26e83834454ed126988493573@95.216.74.4:26656,9f993f07f3fe0c788f7d55f88b7a031028a378f5@217.76.60.46:26656,8d16516f31ac536764f15214b99962f30f390b1d@38.242.255.250:26656,acec47a370e278dba9736378c7ecd3c2f5eadef5@194.163.184.70:26656"
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


- **İsteğe bağlı snap kullanabilirsiniz (1,245,371)**

```
sudo systemctl stop nibid

cp $HOME/.nibid/data/priv_validator_state.json $HOME/.nibid/priv_validator_state.json.backup 

nibid tendermint unsafe-reset-all --home $HOME/.nibid --keep-addr-book 
curl https://snapshots2-testnet.nodejumper.io/nibiru-testnet/nibiru-itn-1_2023-03-24.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.nibid

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



















