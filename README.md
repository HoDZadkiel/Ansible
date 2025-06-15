# Ansible
此倉庫僅為個人學習使用，若造成伺服器穩定性問題一蓋不負責

## 特色 (Features):
1. 所有docker部屬能用就用docker-compose
2. 所有docker應用都用volume的方式儲存資料

## 暫定目標 (Tentative Goals):
1. Docker-ce部屬自動化
2. Docker常用軟體部屬自動化
3. 虛擬機管理行為自動化

## 如何使用 (How to Use)

### Prerequisites:
*   Ansible 2.9 或更高版本 (某些模組可能需要特定版本，但 2.9 是一個良好的基準)。
*   目標主機：主要為基於 Linux 的系統 (apt 相關的 playbook 相容於 Debian/Ubuntu，Docker 通常可在各種 Linux 發行版上運行)。
*   受管節點上的 Python 3 (Ansible 模組通常需要)。

### General Steps:
1.  克隆此儲存庫。
2.  建立或更新您的 inventory 檔案 (例如，基於稍後將添加的 `inventory.example`)。
3.  根據需要檢閱和自訂 playbook 變數。
4.  使用 `ansible-playbook -i <your_inventory_file> <playbook_name.yml>` 運行 playbooks。

## 劇本結構 (Playbook Structure)
*   `playbooks/Common`: 包含常用的工具型 playbook，例如 ping 主機。
*   `playbooks/Docker-deploy`: 包含用於安裝 Docker 及將應用程式部署為 Docker 容器的 playbook。
*   `playbooks/VM-deploy`: 包含用於管理虛擬機的 playbook，例如系統更新和磁碟初始化。

## 重點劇本說明 (Key Playbook Explanations)
*   `playbooks/Docker-deploy/Docker-install.ansible.yml`:
    *   用途: 在目標主機上安裝 Docker CE (Community Edition)。
    *   關鍵變數: 使用者應檢查 playbook 以了解可配置的變數。
*   `playbooks/Docker-deploy/Docker-MariaDB-Deploy.ansible.yml`:
    *   用途: 將 MariaDB 伺服器部署為 Docker 容器。強調使用 volume 實現數據持久化。
    *   關鍵變數: 使用者應檢查 playbook 以了解諸如 `mariadb_root_password`、`mariadb_database`、`mariadb_user`、`mariadb_password` 和 `mariadb_data_volume` 等常見變數 (或實際 playbook 中可能存在的等效變數)。
*   `playbooks/VM-deploy/apt-upgrade.ansible.yml`:
    *   用途: 在基於 Debian/Ubuntu 的系統上使用 `apt` 更新軟體包列表並升級已安裝的軟體包。
    *   關鍵變數: 通常沒有，但建議檢閱任務內容。
