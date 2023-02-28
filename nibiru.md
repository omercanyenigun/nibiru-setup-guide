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
PEERS="ac163da500a9a1654f5bf74179e273e2fb212a75@65.108.238.147:27656,abab2c6f45fa865dc61b2757e21c5d2244e5bacb@213.202.218.55:26656,fe17db7c9a5f8478a2d6a39dbf77c4dc2d6d7232@5.75.189.135:26656,baff3597ebd19ce273b7c0b56e2d50a8964d1423@65.109.90.166:26656,ca6213c897bd8400d8d01b947a541db85ebb2d96@51.89.199.49:36656,63256b5937ac438e3b21b570a07ace6ddc3bd0c6@194.163.182.122:39656,c1b40d056e4260a9fa9d1142af1adbeec5039599@142.132.202.50:46656,ea44a000ee4df9d722a90fdf41b3990e738bdda0@65.109.235.95:26656,7e75b2249d088a4dfc3b33f386c316cb47366d2b@195.3.221.48:11656,e08089921baf39382920a4028db9e5eebd82f3d7@142.132.199.236:21656,bb370c5f0a27342913253bf9edf84284378843d6@104.248.18.40:26656,9946c87d01312752d26fe0ceef4f4e24707f8144@65.109.88.178:27656,3f82fd9d86f46715f3fa884bde5107196bb40673@170.187.166.177:26656,4f1af4f62f76c095d844384a3dfa1ad76ad5c078@65.108.206.118:60656,6052d09554a442f22f71c33dbc5f25bee538e087@65.109.82.249:28656,c4124e6623529b31b8c535be1ea8835aa7ff51b0@51.79.77.103:28656,2dce4b0844754b467ae40c9d6360ac51836fadca@135.181.221.186:29656,c8907a13b012e7a937cfe7d624b0fbe7ef3508b2@194.163.160.155:26656,0ebf64601e93d0e5304da8b7d3deb96d7d7cbcf8@176.120.177.123:26656,30e14f66fc44a55a51f36693afd754283c668953@65.108.200.60:11656,fa5c730d842aff05c3761d9c1b06107340ac7651@65.108.232.238:11656,f01ad3a75b255226499df9183ac2ebc0a40a9e05@46.4.53.207:33656,81a8383eefae628ae4bc400d52d49adfb11cb76a@65.108.108.52:11656,1c548375968f0abfac3733cae9f592468c988bf9@46.4.53.209:33656,f4a6bcbd4af5cfd82ee3a40c54800176e33e9477@31.220.79.15:26656,b03d1ce3e97984a8b8a63a7a6ec6c5d196d81436@46.4.53.208:33656,e74f1204d65d0264547e2c2d917c23c39fcff774@95.217.107.96:36656,b316ff6b5a0715732fa02f990db94aef39e758b3@148.251.88.145:10156,79e2bfc202e39ba2a168becc4c75cb6a56803e38@135.181.57.104:11656,68db528df52c31ddec2a98d6331eb888ebcc7d70@114.246.194.91:2526,2686c58fc276fff2956bf1b10736244737f84c9b@178.208.86.44:26656,6c18473eb1d5d3202ea0fcf2c7240eb99233f39d@65.21.245.161:26656,84d888be939b738d343db0613d4cc50a33f36beb@158.101.208.86:26656,21ad250f917fafcd9bca8ea223558dffc6bd75c4@38.242.205.18:26656,1848442cbab24bc7123ad2dec2464661b5bc92c1@94.190.90.38:28656,86c31da7c48f5432889a573e9e1afcfd9fb61af4@193.46.243.74:27656,a08e5b25443d038b08230177456ee23196509dd5@65.109.92.79:12656,10382838df100f7817eb9c86c5da67160eefe4fc@95.216.100.241:30656,62d93ddd046e8092c3717117484ed680cbacbf0d@139.59.239.43:26656,f29c808ff578c7f3a3746b9b0b3e0504b3ee2315@65.108.216.139:26656,8ebed484e09f93b12be00b9f6faa55ea9b13b372@45.84.138.66:39656,4f1c8f3de055988bf15f21b666369287fb5230de@31.220.73.148:26656,c2c2af737665fafa38b52110e591687558fe788a@31.220.78.187:26656,aad0d897a82880e36bb909091c5878607446ab41@138.201.204.5:35656,5f3394bae3791bcb71364df80f99f22bd33cc2c0@95.216.7.169:60556,e9b25db508b31cb9d48b1f0b67147faf8c2b7b0b@65.108.199.206:27656"
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


- **İsteğe bağlı snap kullanabilirsiniz**

```
sudo systemctl stop nibid
nibid tendermint unsafe-reset-all --home $HOME/.nibid --keep-addr-book
curl -L https://snap.nodeist.net/t/nibiru/nibiru.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.nibid --strip-components 2
sudo systemctl start nibid && journalctl -u nibid -f --no-hostname -o cat
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



















