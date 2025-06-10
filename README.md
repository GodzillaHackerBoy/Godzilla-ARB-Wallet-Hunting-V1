⭐Godzilla ARB Wallet Hunting V1 
⤵哥斯拉区块链钱包助记词碰撞器/密钥碰撞器（ARB链）
▶https://youtu.be/x5LV55UPLT8
⬇https://mega.nz/file/mVNkVZ5J#rg_4bdv3rXTv-YwifeGD6dBC1bzxNG4xnKpQk7F0NRQ

这是一个用于生成和检查ARB(Arbitrum)链钱包地址的Python工具
## 核心功能
### 1. 助记词生成
工具使用 mnemonic 库生成符合BIP39标准的12个单词助记词：
def generate_mnemonic():
    """生成助记词"""
    mnemo = Mnemonic("english")
    return mnemo.generate(strength=128)

### 2. ARB地址生成
通过 eth_account 库从助记词派生ARB链地址：
def generate_arb_address(mnemonic):
    """生成ARB链地址"""
    Account.enable_unaudited_hdwallet_features()
    acct = Account.from_mnemonic(mnemonic)
    return acct.address

### 3. 多线程钱包生成
使用QThread实现后台钱包生成：
class WalletWorker(QThread):
    update_signal = pyqtSignal(str, str, int)
    def run(self):
        count = 0
        while self.is_running:
            mnemonic = generate_mnemonic()
            addr = generate_arb_address(mnemonic)
            if addr:
                count += 1
                self.update_signal.emit(mnemonic, addr, count)
                

