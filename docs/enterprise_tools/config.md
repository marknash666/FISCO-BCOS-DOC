# 配置文件介绍

FISCO BCOS generator的配置文件在./conf文件夹下，配置文件为：群组创世区块配置文件`group_genesis.ini`和生成节点配置文件`node_deployment.ini`。

用户通过对conf文件夹下文件的操作，配置生成节点配置文件夹的具体信息。

## 元数据文件夹meta

FISCO BCOS generator的meta文件夹为元数据文件夹，需要存放`fisco bcos`二进制文件、链证书`ca.crt`、本机构机构证书`agency.crt`、机构私钥节点证书、群组创世区块文件等。

证书的存放格式需要为cert_p2pip_port.crt的格式，如cert_127.0.0.1_30300.crt。

FISCO BCOS generator会根据用户在元数据文件夹下放置的相关证书、conf下的配置文件，生成用户下配置的节点配置文件夹。

## group_genesis.ini

通过修改`group_genesis.ini`的配置，用户在指定目录及meta文件夹下生成新群组创世区块的相关配置，如`group.1.genesis`。

```ini
[group]
group_id=1

[nodes]
node0=127.0.0.1:30300
;群组创世区块的节点p2p地址
node1=127.0.0.1:30301
node2=127.0.0.1:30302
node3=127.0.0.1:30303
```

```eval_rst
.. important::
    生成群组创世区块时需要节点的证书，如上述配置文件中需要4个节点的证书。分别为：cert_127.0.0.1_30301.crt，cert_127.0.0.1_30302.crt，cert_127.0.0.1_30303.crt和cert_127.0.0.1_30304.crt。
```

## node_deployment.ini

通过修改`node_deployment.ini`的配置，用户可以使用--build_install_package命令在指定文件夹下生成节点不含私钥的节点配置文件夹。用户配置的每个`section[node]`即为用户需要生成的节点配置文件夹.`section[peers]`为需要连接的其他节点p2p信息。

配置文件示例如下：

```ini
[group]
group_id=1

# Owned nodes
[node0]
p2p_ip=127.0.0.1
rpc_ip=127.0.0.1
p2p_listen_port=30300
channel_listen_port=20200
jsonrpc_listen_port=8545

[node1]
p2p_ip=127.0.0.1
rpc_ip=127.0.0.1
p2p_listen_port=30301
channel_listen_port=20201
jsonrpc_listen_port=8546
```

上述配置在执行build命令后会在指定目录下生成名为node_127.0.0.1_30300、node_127.0.0.1_30301的配置文件夹。生成的节点处于群组group1中。

```eval_rst
.. note::
    生成节点配置文件夹时只需要自己节点的证书，如上述操作中，需要的证书为：cert_127.0.0.1_30300.crt和cert_127.0.0.1_30301.crt
```