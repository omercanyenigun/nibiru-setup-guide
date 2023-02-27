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
go version
```

- **Binary Yüklemesi**

```
cd $HOME
rm -rf nibiru
git clone https://github.com/NibiruChain/nibiru.git
cd nibiru
git checkout v0.19.2
make build
```

- **nibid'ün başarılı yüklendiğinin kontrolü**

```
nibid version
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

- **Genesis ve addrbook'u indirme**

```
wget https://raw.githubusercontent.com/omercanyenigun/nibiru-setup-guide/main/genesis.json -O $HOME/.nibid/config/genesis.json
```

- **Seeds ve Peers'i Yapılandırma**

```
SEEDS="a431d3d1b451629a21799963d9eb10d83e261d2c@seed-1.itn-1.nibiru.fi:26656,6a78a2a5f19c93661a493ecbe69afc72b5c54117@seed-2.itn-1.nibiru.fi:26656"
PEERS="e2b8b9f3106d669fe6f3b49e0eee0c5de818917e@213.239.217.52:32656,930b1eb3f0e57b97574ed44cb53b69fb65722786@144.76.30.36:15662,ad002a4592e7bcdfff31eedd8cee7763b39601e7@65.109.122.105:36656,4a81486786a7c744691dc500360efcdaf22f0840@15.235.46.50:26656,68874e60acc2b864959ab97e651ff767db47a2ea@65.108.140.220:26656,d5519e378247dfb61dfe90652d1fe3e2b3005a5b@65.109.68.190:39656"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.nibid/config/config.toml
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
















