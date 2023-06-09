## SSH

SSH（Secure Shell）是一種安全的網路協定，預設是走 22 port，
推薦使用此方式 clone 專案，早期是使用 HTTPS 方式 clone 專案，每次更新 push 到遠端儲存庫都要輸入 username 和 password 才能推上遠端。

使用以下 SSH 的方式，只要你的公鑰有設置在遠端儲存庫，伺服器就能知道你的身份。

在 SSH 中，非對稱加密使用了一對密鑰，即公鑰和私鑰。公鑰是公開的，可以被任何人使用，而私鑰是保密的，只能由擁有者訪問。公鑰和私鑰是密碼學上相互關聯的，對於一個公鑰，只有唯一的私鑰可以對其進行解密，而對於一個私鑰，只有唯一的公鑰可以對其進行加密。

服務器會使用客戶端公鑰加密一個隨機生成的會話密鑰，並將其發送給客戶端。客戶端使用其私鑰解密會話密鑰，然後使用對稱加密算法（如 AES）將通信數據加密，然後發送到服務器。服務器使用相同的對稱加密算法解密通信數據，以及用於驗證數據完整性的消息驗證碼（MAC）。

使用非對稱加密的好處是，即使公鑰被泄露，黑客也無法使用公鑰來解密通信數據。因為唯一能夠解密通信數據的是私鑰，而私鑰在系統中是只有擁有者可以訪問的。

### 產生一組 ssh

MacOS、Windows、Linux 都可以透過以下指令產生一組非對稱式的公私鑰。

其中 `-C "key_name"` 是用來標示這把 key 的名稱，不標示也行。

`-t ed25519` 則是將演算法指定為 ed25519 ，是目前常用的公鑰格式。相比預設的 RSA 演算法，公鑰長度會比較短。

```bash
ssh-keygen -t ed25519 -C "key_name"
```

一開始會詢問這把 key 預設會產生名為 `id_ed25519` 的檔案在 `~/.ssh/` 資料夾底下。

如果要改地方可以在產生的時候，指定位置，像是我這邊是指定當前資料夾 `./id_ed25519`。

然後一直按 Enter 就可以產生名為 id_ed25519 的私鑰和 id_ed25519.pub 的公鑰。

```bash
Generating public/private ed25519 key pair.
Enter file in which to save the key (~/.ssh/id_ed25519): ./id_ed25519
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ./id_ed25519
Your public key has been saved in ./id_ed25519.pub
The key fingerprint is:
SHA256:x7CDEGANxQ1jXPWh7ClRTWX1BwhryyQpwIOhFYXhyVI keyname
The key's randomart image is:
+--[ED25519 256]--+
|  E/O+..oo+oooo  |
| Boo*+.o +.+.  o |
|o + ..o * =     o|
| .   . = X .    .|
|      o S =      |
|       . o       |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```

## 設定公鑰在伺服器上

在 Github 可以在 https://github.com/settings/keys 設定你的公鑰，如果你有多台電腦的話，可以考慮命名清楚。這樣在不同電腦使用 SSH 與 Github 伺服器溝通就不用一直輸入密碼。

![public_key](https://github.com/Luca-Lin/git-practice/blob/main/images/remote/public_key.png)
