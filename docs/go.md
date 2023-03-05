## install golang

```bash
wget https://go.dev/dl/go1.20.1.linux-amd64.tar.gz

sudo su

rm -rf /usr/local/go && tar -C /usr/local -xzf go1.20.1.linux-amd64.tar.gz

exit

echo "export GOPATH=~/Documents/repository/go/" >> ~/.bashrc
echo "export GOBIN=~/Documents/repository/go/bin" >> ~/.bashrc

echo "export PATH=$PATH:$GOPATH:$GOBIN" >> ~/.bashrc

go version
```