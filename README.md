# Stride Testnet-4 Kurulum Rehberi

<img width="431" alt="stride111" src="https://user-images.githubusercontent.com/107190154/184557695-bc92418f-1eb8-4514-ae06-d89802efda9a.png">

> Not: Şu an kurduğumuz direkt chain-4


### Sistem Gereksinimleri 

|CPU | RAM  | Disk  | 
|----|------|----------|
|   4| 8GB  | 250GB    |

 # Daha önce Node kurulumu yapmadıysanız buradan sırasıyla adımları takip ederek tüm süreci öğrenebilirsiniz.
  ## Yeni Başladım Rehberi; [Pusula Finans Labs.](https://www.labs.pusulafinans.com/category/rehber/)
  ### 1. [Testnet ve Node test kurulum rehberi Bölüm-1](https://www.labs.pusulafinans.com/2022/08/23/testnet-ve-node-kurulum-rehberi/)
  ### 2. [Yeni Chrome Tarayıcı nasıl açarım?](https://www.labs.pusulafinans.com/2022/08/23/yeni-chrome-tarayici-nasil-acarim/)
  ### 3. [Ücretsiz Sunucu Kiralama](https://www.labs.pusulafinans.com/2022/08/23/nasil-ucretsiz-sunucu-kiralarim/)
  ### 4. [Digital Ocean Nasıl Kayıt olurum?](https://www.labs.pusulafinans.com/2022/08/23/digital-oceana-nasil-kayit-olabilirim/)
  ### 5. [MobaXTerm Terminal Kurulumu](https://www.labs.pusulafinans.com/2022/08/23/mobaxterm-terminal-kurulumu/)
  
### Kuruluma başlayalım.

```
wget -O stride.sh https://raw.githubusercontent.com/pusulafinanslabs/Stride-Testnet-4/main/stride.sh && chmod +x stride.sh && ./stride.sh
```

### Log kontrol komutundan sonra log komutu tepki vermiyorsa şu komutu girip ardından yeniden log kontrol yapın.

```
systemctl restart systemd-journald
```

### Sync Durumunuzu öğrenmek için;

```
strided status 2>&1 | jq .SyncInfo
```

### Faucet için; Discorda katılmayı unutmayın. ( https://discord.gg/ggQewkUa )

### Validator Olmak İçin;

```
strided tx staking create-validator \
  --amount 9900000ustrd \
  --from cüzdanisminiz \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(strided tendermint show-validator) \
  --moniker nodeisminiz \
  --chain-id=STRIDE-TESTNET-4 
```

### Explorer

```
https://stride.explorers.guru/
```

### Discorddan Role-Request Odasına Explorerdan validator linkinizi atıp rol almayı unutmayın.

## Stride Önemli Komutlar

### Cüzdandan cüzdana token transfer

```
strided tx bank send gönderencüzdanadresi alıcıcüzdanadresi 1000000ustrd --chain-id=STRIDE-TESTNET-4 --from cüzdanisminiz --fees=250ustrd -y
```

### Kendi validatorumuze delege etme

```
strided tx staking delegate validatorAddress 10000000ustrd --from=WalletName --chain-id=STRIDE-TESTNET-4 --gas=auto
```

### Redelege yapma

```
strided tx staking redelegate gönderenvalidatoradres alıcıvalidatoradres 1000000ustrd --chain-id=STRIDE-TESTNET-4 --from cüzdan --gas=250000 --fees=500ustrd -y
```

### Log kontrol

```
journalctl -u strided -f -o cat
```

### Sync durumu

```
curl -s localhost:16657/status | jq .result.sync_info
```

### Unjail komutu

```
strided tx slashing unjail --from=Cüzdanismi --chain-id=STRIDE-TESTNET-4 --gas-prices=0.025ustrd
```

### Node'u silmek için gerekli komut

```
sudo systemctl stop strided
sudo systemctl disable strided
sudo rm /etc/systemd/system/stride* -rf
sudo rm $(which strided) -rf
sudo rm $HOME/.stride* -rf
sudo rm $HOME/stride -rf
sed -i '/STRIDE_/d' ~/.bash_profile
```

### Kolay Gelsin..

