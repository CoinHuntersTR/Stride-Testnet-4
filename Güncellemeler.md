# 70500. blok ulaşanlar Stride v4.1 güncellemesi yapsın !
```
sudo systemctl stop strided
cd $HOME && rm -rf stride
git clone https://github.com/Stride-Labs/stride.git && cd stride
git checkout 90859d68d39b53333c303809ee0765add2e59dab
make build
sudo mv build/strided $(which strided)
sudo systemctl restart strided && journalctl -fu strided -o cat
```
