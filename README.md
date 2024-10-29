# Nexus

> Nexus için kontrat deploylayıp dosylarımı yedekledim.

> Bir beklentim yok bir kaç dakikalık işlem diye yapıyorum.

> Herhangi bir sunucuda yapabilirsiniz. 

<details>
  <summary> <h1> Yatırımı hakkında </summary> </h1>

![image](https://github.com/ruesandora/Nexus/assets/101149671/9fcbe5d7-d88c-49b8-af65-768132f75176)

</details>

# Kurulum

```console
# güncelleme
sudo apt update -y && sudo apt upgrade -y
sudo apt install cmake
sudo apt install build-essential
```

#

```console
# rustup kurulumu

# 1 seçeneğini seçiyoruz
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# rust kurulumu tamamlandıktan sonra
. "$HOME/.cargo/env"
rustup target add riscv32i-unknown-none-elf
```

#

```console
# nexus tool kurulumu

# burası biraz uzun sürer - hatalar görürseniz sorun yok.
cargo install --git https://github.com/nexus-xyz/nexus-zkvm cargo-nexus --tag 'v0.2.3'

# nexus oluşturuyoruz
cargo nexus new nexus-project

# main.rs değiştireceğiz
cd nexus-project
```

#

```console

# bu dosyaya giriyoruz
nano ./src/main.rs
# içersindeki kodları silip aşağıdaki bloğu girin
```

```console
#![no_std]
#![no_main]

fn fib(n: u32) -> u32 {
    match n {
        0 => 0,
        1 => 1,
        _ => fib(n - 1) + fib(n - 2),
    }
}

#[nexus_rt::main]
fn main() {
    let n = 7;
    let result = fib(n);
    assert_eq!(result, 13);
}
```

#

```console
# contratı run edelim
cargo nexus run
cargo nexus run -v

# prove etmeseini bekleyelim işlemlerin
cargo nexus prove

# verify işlemini tamamlayalım
cargo nexus verify
```

#

> Bu dizinde ki `nexus-proof`dosyamızı kaydedip saklayalım

<img width="417" alt="Ekran Resmi 2024-06-14 11 02 40" src="https://github.com/ruesandora/Nexus/assets/101149671/b6468869-3274-4b05-857d-a82263729585">


# Network Cli
Screen açıp kodu çalıştıralım. Yeni bir versiyonu varsa ilk önce onu indirecek


```console
screen -S nexus
curl https://cli.nexus.xyz/ | sh
```

Bir süre bekledikten sonra ctrl A D ile kapatabilirsin.
İşlem başarılı olduysa ```prover-id```  ```/root/.nexus/``` konumundan alabilirsin.  


> bu kadardı işlemler.
