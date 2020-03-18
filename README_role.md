# Ansible Role: Apache\_setup

## Description
本Ansible RoleはWebサーバソフトウェアである"Apache HTTP Server"の初期設定を行います。
対象バージョンは以下のバージョンです。

- Apache2.2 (RHEL6)
- Apache2.4 (RHEL7)

以下のファイルを設定します。
- /etc/httpd/conf/httpd.conf
- /etc/httpd/conf.d/proxy.conf

## Supports

- 管理マシン(Ansibleサーバ)
  * Linux系OS（RHEL/CentOS）
  * Ansible バージョン 2.0 以上
  * Python バージョン 2.6 または2.7

- 管理対象マシン(構築対象マシン)
  * RHEL6、RHEL7

## Requirements

- 管理マシン(Ansibleサーバ)
  * 管理対象マシンとroot権限でSSH通信可能であること。

- 管理対象マシン(インストール対象マシン)
  * Red Hat提供パッケージからApache(httpd,httpd-tools)がインストールされていること
  * SELinuxが無効に設定されていること
  * iptables,firewalldが適切に設定されていること

## Role Variables

Role の変数値について説明します。

### Mandatory variables

実行時には、必ず指定しないといけない変数はありません。

### Optional variables

以下の変数は任意で指定します。

- 標準ディレクティブ設定・Apache2.2(RHEL6)の場合
  * ''VAR_Apache_ServerTokens'': ServerTokens(string, default: "OS")
  * ''VAR_Apache_ServerRoot'': ServerRoot(string, default: "/etc/httpd")
  * ''VAR_Apache_PidFile'': PidFile(string, default: "run/httpd.pid")
  * ''VAR_Apache_Timeout'': Timeout(number, default: "60")
  * ''VAR_Apache_KeepAlive'': KeepAlive("On"|"Off", default: "Off")
  * ''VAR_Apache_MaxKeepAliveRequests'': MaxKeepAliveRequests(number, default: "100")
  * ''VAR_Apache_KeepAliveTimeout'': KeepAliveTimeout(number, default: "15")
  * ''VAR_Apache_Listen'': Listen(number, default: "80")
  * ''VAR_Apache_ExtendedStatus'': ExtendedStatus(string, default: "")
  * ''VAR_Apache_User'': User(string, default: "apache")
  * ''VAR_Apache_Group'': Group(string, default: "apache")
  * ''VAR_Apache_ServerAdmin'': ServerAdmin(string, default: "root@localhost")
  * ''VAR_Apache_ServerName'': ServerName(string, default: "")
  * ''VAR_Apache_UseCanonicalName'': UseCanonicalName("On"|"Off", default: "Off")
  * ''VAR_Apache_DocumentRoot'': DocumentRoot(string, default: "/var/www/html")
  * ''VAR_Apache_DirectoryIndex'': DirectoryIndex(string, default: "index.html index.html.var")
  * ''VAR_Apache_AccessFileName'': AccessFileName(string, default: ".htaccess")
  * ''VAR_Apache_TypesConfig'': TypesConfig(string, default: "/etc/mime.types")
  * ''VAR_Apache_DefaultType'': DefaultType(string, default: "text/plain")
  * ''VAR_Apache_MIMEMagicFile'': MIMEMagicFile(string, default: "conf/magic")
  * ''VAR_Apache_HostnameLookups'': HostnameLookups("On"|"Off", default: "Off")
  * ''VAR_Apache_ErrorLog'': ErrorLog(string, default: "log/error_log")
  * ''VAR_Apache_LogLevel'': LogLevel(string, default: "warn")
  * ''VAR_Apache_LogFormat'': LogFormat(string, default: "")
    + 設定値には「'」を付与してください。(例:' "%h %l %u %t \"%r\" %>s %b" common ')
  * ''VAR_Apache_CustomLog'': CustomLog(string, default: "logs/access_log combined")
  * ''VAR_Apache_ServerSignature'': ServerSignature(string, default: "On")
  * ''VAR_Apache_IndexOptions'': IndexOptions(string, default: "FancyIndexing VersionSort NameWidth=* HTMLtable Charset=UTF-8")
  * ''VAR_Apache_AddDefaultCharset'': AddDefaultCharset(string, default: "UTF-8")
  * ''VAR_Apache_EnableMMAP'': EnableMMAP("On"|"Off", default: "")
  * ''VAR_Apache_EnableSendfile'': EnableSendfile("On"|"Off", default: "")

- 標準ディレクティブ設定・Apache2.4(RHEL7)の場合
  * ''VAR_Apache_ServerTokens'': ServerTokens(string, default: "")
  * ''VAR_Apache_ServerRoot'': ServerRoot(string, default: "/etc/httpd")
  * ''VAR_Apache_Timeout'': Timeout(number, default: "")
  * ''VAR_Apache_KeepAlive'': KeepAlive("On"|"Off", default: "")
  * ''VAR_Apache_MaxKeepAliveRequests'': MaxKeepAliveRequests(number, default: "")
  * ''VAR_Apache_KeepAliveTimeout'': KeepAliveTimeout(number, default: "")
  * ''VAR_Apache_Listen'': Listen(number, default: "80")
  * ''VAR_Apache_ExtendedStatus'': ExtendedStatus(string, default: "")
  * ''VAR_Apache_User'': User(string, default: "apache")
  * ''VAR_Apache_Group'': Group(string, default: "apache")
  * ''VAR_Apache_ServerAdmin'': ServerAdmin(string, default: "root@localhost")
  * ''VAR_Apache_ServerName'': ServerName(string, default: "")
  * ''VAR_Apache_UseCanonicalName'': UseCanonicalName("On"|"Off", default: "")
  * ''VAR_Apache_DocumentRoot'': DocumentRoot(string, default: "/var/www/html")
  * ''VAR_Apache_DirectoryIndex'': DirectoryIndex(string, default: "index.html index.html.var")
  * ''VAR_Apache_AccessFileName'': AccessFileName(string, default: "")
  * ''VAR_Apache_TypesConfig'': TypesConfig(string, default: "/etc/mime.types")
  * ''VAR_Apache_MIMEMagicFile'': MIMEMagicFile(string, default: "conf/magic")
  * ''VAR_Apache_HostnameLookups'': HostnameLookups("On"|"Off", default: "")
  * ''VAR_Apache_ErrorLog'': ErrorLog(string, default: "log/error_log")
  * ''VAR_Apache_LogLevel'': LogLevel(string, default: "warn")
  * ''VAR_Apache_LogFormat'': LogFormat(string, default: "")
    + 設定値には「'」を付与してください。(例:' "%h %l %u %t \"%r\" %>s %b" common ')
  * ''VAR_Apache_LogFormat_IO'': LogFormat(string, default: "")
    + 設定値には「'」を付与してください。(例:' "%h %l %u %t \"%r\" %>s %b" common ')
    + IO関連オプション（「%I」,「%O」）を指定することができます。
    + mod_log_config  モジュールが必要です。
  * ''VAR_Apache_CustomLog'': CustomLog(string, default: "logs/access_log combined")
  * ''VAR_Apache_ServerSignature'': ServerSignature(string, default: "")
  * ''VAR_Apache_AddDefaultCharset'': AddDefaultCharset(string, default: "UTF-8")
  * ''VAR_Apache_EnableMMAP'': EnableMMAP("On"|"Off", default: "")
  * ''VAR_Apache_EnableSendfile'': EnableSendfile("On"|"Off", default: "On")

- Tomcat連携ディレクティブ設定
  * ''VAR_Apache_Proxy'': ProxyPass(on|off, default: "")
      + Tomcat連携ディレクティブを有効にするためには、"on"を指定します。
      + デフォルトもしくは、"off"を指定した場合は、Tomcat連携ディレクティブが有効になりません。
  * ''VAR_Apache_ProxyPass'': ProxyPass(string[], default: "")
  * ''VAR_Apache_ProxyPassReverse'': ProxyPassReverse(string[], default: "")
  * ''VAR_Apache_ProxyPassReverseCookieDomain'': ProxyPassReverseCookieDomain(string[], default: "")
  * ''VAR_Apache_ProxyPassReverseCookiePath'': ProxyPassReverseCookiePath(string[], default: "")
  * ''VAR_Apache_ProxyPassMatch'': ProxyPassMatch(string[], default: "")
  * ''VAR_Apache_ProxySet'': ProxySet(string, default: "")
  * ''VAR_Apache_ProxyBadHeader'': ProxyBadHeader(string, default: "")
  * ''VAR_Apache_ProxyBlock'': ProxyBlock(string, default: "")
  * ''VAR_Apache_ProxyDomain'': ProxyDomain(string, default: "")
  * ''VAR_Apache_ProxyErrorOverride'': ProxyErrorOverride("On"|"Off", default: "")
  * ''VAR_Apache_ProxyIOBufferSize'': ProxyIOBufferSize(number, default: "")
  * ''VAR_Apache_ProxyMaxForwards'': ProxyMaxForwards(number, default: "")
  * ''VAR_Apache_ProxyPassInterpolateEnv'': ProxyPassInterpolateEnv("On"|"Off", default: "")
  * ''VAR_Apache_ProxyPreserveHost'': ProxyPreserveHost("On"|"Off", default: "")
  * ''VAR_Apache_ProxyReceiveBufferSize'': ProxyReceiveBufferSize(number, default: "")
  * ''VAR_Apache_ProxyStatus'': ProxyStatus("On"|"Off", default: "")
  * ''VAR_Apache_ProxyTimeout'': ProxyTimeout(number, default: "")
  * ''VAR_Apache_ProxyVia'': ProxyVia("On"|"Off"|"Full"|"Block", default: "")
  * ''VAR_Apache_ProxyAddHeaders'': ProxyAddHeaders("On"|"Off", default: "") (RHEL7のみ)
  * ''VAR_Apache_ProxyPassInherit'': ProxyPassInherit("On"|"Off", default: "") (RHEL7のみ)
  * ''VAR_Apache_ProxySourceAddress'': ProxySourceAddress(string, default: "") (RHEL7のみ)

- MPMの設定
  * ''VAR_Apache_MPMType': 利用するMPM種別(prefork|worker|event, default: "prefork")
   + Apache2.2の場合、 "prefork"、"worker"から選択
   + Apache2.4の場合、 "prefork"、"worker"、"event"から選択
  * preforkの場合
   + ''VAR_Apache_StartServers'': StartServers(number, default: "8")
   + ''VAR_Apache_MinSpareServers'': MinSpareServers(number, default: "5")
   + ''VAR_Apache_MaxSpareServers'': MaxSpareServers(number, default: "20")
   + ''VAR_Apache_ServerLimit'': ServerLimit(number, default: "256")
   + ''VAR_Apache_MaxClients'': MaxClients(number, default: "256") (RHEL6のみ)
   + ''VAR_Apache_MaxRequestWorkers'': MaxRequestWorkers(number, default: "256") (RHEL7のみ)
   + ''VAR_Apache_MaxRequestsPerChild'': MaxRequestsPerChild(number, default: "4000") (RHEL6のみ)
   + ''VAR_Apache_MaxConnectionsPerChild'': MaxConnectionsPerChild(number, default: "4000") (RHEL7のみ)
 * workerの場合
   + ''VAR_Apache_StartServers'': StartServers(number, default: "4")
   + ''VAR_Apache_MaxClients'': MaxClients(number, default: "300") Apache2.2のみ
   + ''VAR_Apache_MaxRequestWorkers'': MaxRequestWorkers(number, default: "300") (RHEL7のみ)
   + ''VAR_Apache_MinSpareThreads'': MinSpareThreads(number, default: "25")
   + ''VAR_Apache_MaxSpareThreads'': MaxSpareThreads(number, default: "75")
   + ''VAR_Apache_ThreadsPerChild'': ThreadsPerChild(number, default: "25")
   + ''VAR_Apache_MaxRequestsPerChild'': MaxRequestsPerChild(number, default: "0") (RHEL6のみ)
   + ''VAR_Apache_MaxConnectionsPerChild'': MaxConnectionsPerChild(number, default: "0") (RHEL7のみ)
 * eventの場合 (RHEL7のみ)
   + ''VAR_Apache_StartServers'': StartServers(number, default: "4")
   + ''VAR_Apache_MinSpareThreads'': MinSpareThreads(number, default: "25")
   + ''VAR_Apache_MaxSpareThreads'': MaxSpareServers(number, default: "75")
   + ''VAR_Apache_ThreadsPerChild'': ThreadsPerChild(number, default: "25")
   + ''VAR_Apache_MaxRequestWorkers'': MaxRequestWorkers(number, default: "300")
   + ''VAR_Apache_MaxConnectionsPerChild'': MaxConnectionsPerChild(number, default: "0")

- サービス自動起動設定
   + ''VAR_Apache_ServiceState'': httpd起動・停止(started|stopped|restarted, default:"stoped")
   + ''VAR_Apache_ServiceAuto'': サービス自動起動(yes|no, default:"no")

- 注意事項
  * パラメータに、OnまたはOffを指定する場合は、"(ダブルクォート)を付与してください。(ex:"On","Off")

## Dependencies

特にありません。

## Usage

1. 本Roleを用いたPlaybookを作成します。
2. 任意変数を必要に応じて指定します。
3. Playbookを実行します。


## Example Playbook

インストールとすべての設定をする場合は、提供した以下のRoleを"roles"ディレクトリに配置したうえで、
以下のようなPlaybookを作成してください。

- フォルダ構成
~~~
  - group_vars/
    ・ server1
    ・ server2
  - host_vars/
    ・ host1
    ・ host2
  - roles/
    ・ Apache_install/
    ・ Apache_setup/
  - Apache_install.yml
  - Apache_setup.yml
  - conf.yml
  - hosts
  - site.yml
~~~

- マスターPlaybook サンプル「Apache\_setup.yml」
~~~
# Apache_setup.yml
 - name: setup Apache
   hosts: all
   gather_facts: yes
   become: yes
   tags:
    - setup
   roles:
     - Apache_setup
~~~

## Running Playbook

- extra-varsを利用する場合の実行例
> ansible-playbook site.yml -k -i hosts --extra-vars="@conf.yml"

- group\_varsを利用する場合の実行例   
  group\_varsで指定したグループ名がwebserver1の場合
> ansible-playbook site.yml -k -i hosts -l webserver1

- host\_varsを利用する場合の実行例  
  host\_varsで指定したホスト名がserver1の場合
> ansible-playbook site.yml -k -i hosts -l server1

- 本roleのみを実行する場合は --tags "setup"を付け加える
> ansible-playbook site.yml -k -i hosts --extra-vars="@conf.yml" --tags "setup"

# Copyright
Copyright (c) 2016 NEC Corporation

# Author Information
NEC Corporation

