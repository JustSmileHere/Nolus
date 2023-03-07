# Nolus
Nolust Testnet snapshots guide, Snapshots are updated twice per day. Discord contact: JustSmile#0064

Install lz4
```
apt update
apt upgrade --yes
apt install lz4
```

Stop nolusd service
```
sudo systemctl stop nolusd.service
```

Back-up priv_validator_state.json in order to avoid possible double-sign
```
cp $HOME/.nolus/data/priv_validator_state.json $HOME/priv_validator_state.json
```

Reset database
```
nolusd tendermint unsafe-reset-all --home $HOME/.nolus --keep-addr-book
```

Download and unpack snapshot
```
curl -L http://194.163.189.98/nolus-rila/data.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
curl -L http://194.163.189.98/nolus-rila/wasm.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
```

Restore priv_validator_state.json
```
mv $HOME/priv_validator_state.json $HOME/.nolus/data/priv_validator_state.json
```

Start service
```
sudo systemctl start nolusd.service
```

Check the output of service
```
journalctl -u nolusd.service -f
```
