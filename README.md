# Avail-Goldberg-Update

# Avail kate testnetinde hali hazırda node çalıştırıyorsanız. Bu adımları tamamlayarak Goldberg ağında Node çalıştırabilirsiniz

 Video:

 
1.Install Rust

```
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

2.**Avail dosya konumuna gelip, sistemi durduralım**

```
cd avail
sudo systemctl stop availd.service
```

3..**Git dosyasının yenileyelim ve kontrol edelim**

```
git pull 
git checkout v1.8.0.0
```

4.**Güncelledikten sonra Golberg ağını sistemde başlatalım, Bu yaklaşık 20 dk vs sürmesi gerekiyor**

```
cargo run --locked --release -- --chain goldberg -d ./output
```
5.**Bu işlemden sonra sistem dosyasına girelim**

```
sudo nano /etc/systemd/system/availd.service
```
Burada Description kısmını , -name "honezetwo" node ismini, kendinizin belirlediklerini yapın ve Ctrl +X ile kaydedip çıkın.
```
Description=Honeztwo
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart= /root/avail/target/release/data-avail --base-path `pwd`/data --chain goldberg --name honeztwo
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
```


6. **Yapılan değişiklikleri sistemde kaydedelim**
```
touch /etc/systemd/system/availd.service
nano /etc/systemd/system/availd.service
```
```
systemctl daemon-reload
```


7. **Yararlı Kodlar**


**To enable this to autostart on bootup run:**

```systemctl enable availd.service```

Start it manually with:

```systemctl start availd.service```

You can check that it's working with:

```systemctl status availd.service```

You can tail the logs with journalctllike so:

```journalctl -f -u availd```

Check your node on https://telemetry.avail.tools/
![image](https://github.com/DinhCongTac221/Install-Avail-Full-Node/assets/27664184/c70aaf66-ccbc-485e-ae9e-c09674425772)

