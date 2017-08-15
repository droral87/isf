# 框架介绍
ISF(Industrial Exploitation Framework)，是一款基于python编写的类似metasploit的工控漏洞利用框架。

ISF基于开源项目[routersploit](https://github.com/reverse-shell/routersploit)修改而来。

*该文档的其他语言版本: [English](README.md), [简体中文](README.zh-cn.md),*


## 工控协议客户端
| Name               | Path                                   | Description            |
| -------------------| ---------------------------------------|:----------------------:|  
| modbus_tcp_client  | icssploit/clients/modbus_tcp_client.py | Modbus-TCP客户端工具 |
| wdb2_client        | icssploit/clients/wdb2_client.py       | WdbRPC Version 2 客户端工具(Vxworks 6.x)|


## Exploit 模块
| Name                    | Path                                                              | Description                             |
| ------------------------| ------------------------------------------------------------------|:---------------------------------------:|  
| s7_300_400_plc_control  | exploits/plcs/siemens/s7_300_400_plc_control.py | S7-300/400 PLC 启停脚本                  |
| vxworks_rpc_dos         | exploits/plcs/vxworks/vxworks_rpc_dos.py               | Vxworks RPC 远程拒绝服务（CVE-2015-7599） |
| quantum_140_plc_control | exploits/plcs/schneider/quantum_140_plc_control.py     | Schneider Quantum 140系列 PLC启停脚本    |
| crash_qnx_inetd_tcp_service | exploits/plcs/qnx/crash_qnx_inetd_tcp_service.py | Crash QNX Inetd TCP Service |
| qconn_remote_exec | exploits/plcs/qnx/qconn_remote_exec.py | QNX QCONN 远程代码执行 |


## Scanner 模块
| Name                    | Path                                                              | Description                             |
| ------------------------| ------------------------------------------------------------------|:---------------------------------------:|  
| profinet-dcp-scan       | scanners/profinet-dcp-scan.py                                     | Profinet DCP 扫描器                      |
| vxworks_6_scan          | scanners/vxworks_6_scan.py                                        | Vxworks 6.x 扫描器                       |


## ICS 协议模块 (使用Scapy编写)
这些协议模块能够与其他Fuzz框架进行结合，例如[Kitty](https://github.com/cisco-sas/kitty)或用于编写属于你自己的客户端工具.
 
| Name                    | Path                                                              | Description                             |
| ------------------------| ------------------------------------------------------------------|:---------------------------------------:|  
| pn_dcp                  | icssploit/protocols/pn_dcp                                        | Profinet DCP Protocol                   |
| modbus_tcp              | icssploit/protocols/modbus_tcp                                    | Modbus TCP Protocol                     |
| wdbrpc2                 | icssploit/protocols/wdbrpc2                                       | WDB RPC Version 2 Protocol              |



# 安装

## python依赖环境
* gnureadline (OSX only)
* requests
* paramiko
* beautifulsoup4
* pysnmp
* python-nmap
* scapy [强烈建议参考官方文档手动安装最新版](http://scapy.readthedocs.io/en/latest/installation.html)

## 在Kali 中安装
    git clone https://github.com/dark-lbp/isf/
    cd isf
    python isf.py


# 使用
        root@kali:~/Desktop/temp/isf# python isf.py
        
          _____ _____  _____ _____ _____  _      ____ _____ _______
         |_   _/ ____|/ ____/ ____|  __ \| |    / __ \_   _|__   __|
           | || |    | (___| (___ | |__) | |   | |  | || |    | |
           | || |     \___ \\___ \|  ___/| |   | |  | || |    | |
          _| || |____ ____) |___) | |    | |___| |__| || |_   | |
         |_____\_____|_____/_____/|_|    |______\____/_____|  |_|
        
        
                        ICS Exploitation Framework
        
        Note     : ICSSPOLIT is fork from routersploit at
                   https://github.com/reverse-shell/routersploit
        Dev Team : wenzhe zhu(dark-lbp)
        Version  : 0.1.0
        
        Exploits: 2 Scanners: 0 Creds: 13
        
        ICS Exploits:
            PLC: 2          ICS Switch: 0
            Software: 0
        
        isf >

## Exploits
    isf > use exploits/plcs/
    exploits/plcs/siemens/  exploits/plcs/vxworks/
    isf > use exploits/plcs/siemens/s7_300_400_plc_control
    exploits/plcs/siemens/s7_300_400_plc_control
    isf > use exploits/plcs/siemens/s7_300_400_plc_control
    isf (S7-300/400 PLC Control) >
    
可以使用TAB键来补全路径。

## Options
### 显示 options
    isf (S7-300/400 PLC Control) > show options
    
    Target options:
    
       Name       Current settings     Description
       ----       ----------------     -----------
       target                          Target address e.g. 192.168.1.1
       port       102                  Target Port
    
    
    Module options:
    
       Name        Current settings     Description
       ----        ----------------     -----------
       slot        2                    CPU slot number.
       command     1                    Command 0:start plc, 1:stop plc.
    
    
    isf (S7-300/400 PLC Control) >
    
### 设置 options 参数
    isf (S7-300/400 PLC Control) > set target 192.168.70.210
    [+] {'target': '192.168.70.210'}
    

## 执行module
    isf (S7-300/400 PLC Control) > run
    [*] Running module...
    [+] Target is alive
    [*] Sending packet to target
    [*] Stop plc
    isf (S7-300/400 PLC Control) >
    
## 显示module信息
    isf (S7-300/400 PLC Control) > show info
    
    Name:
    S7-300/400 PLC Control
    
    Description:
    Use S7comm command to start/stop plc.
    
    Devices:
    -  Siemens S7-300 and S7-400 programmable logic controllers (PLCs)
    
    Authors:
    -  wenzhe zhu <jtrkid[at]gmail.com>
    
    References:
    
    isf (S7-300/400 PLC Control) >
    
# 说明文档
* [Modbus-TCP客户端工具使用说明](docs/modbus_tcp_client.zh-cn.md)
* [WDBRPCV2客户端工具使用说明](docs/wdbrpc_v2_client.zh-cn.md)
* [SNMP爆破工具使用说明](docs/snmp_bruteforce.zh-cn.md)
* [从额外的目录中读取modules](docs/load_extra_modules_from_folder.zh-cn.md)
* [如何创建一个module](docs/how_to_create_module.zh-cn.md)