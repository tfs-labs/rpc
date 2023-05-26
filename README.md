# RPC Interface Documentation

This document is an RPC interface document for TFSC,This document is an RPC interface document for TFSC. You can log in [Transformers Labs (github.com)](https://github.com/tfs-labs) to get code for compilation and obtain program.The document which is applicable to TFSC version 0.25.0 introduces some commonly used information acquisition interfaces, transaction interfaces, and callback interfaces.

## Enable RPC interface (important)

Before starting the program,first open the configuration file (config.json) and refer to the following configuration

```C++
{
    "http_callback": {
        "ip": "",
        "path": "",
        "port": 0
    },
    "http_port": 41517,// The default port is 41517
    "info": {
        "logo": "",
        "name": ""
    },
    "ip": "",//Fill in the external network IP address here. If it is not an external network, the network connection cannot be reached
    "log": {
        "console": false,
        "level": "OFF",
        "path": "./logs"
    },
    "rpc": true,//Rpc must be set to true, otherwise the rpc interface cannot be called
    "server": [//Fill in the scout node here
    ],
    "server_port": 41516,//The default port is 41516
    "version": "1.0"
}
```

If you need to enable the rpc function, please modify the config.json file and set 'rpc' to 'true'`

```C++
 "rpc": true,
```

Note: All requests are made through POST

## Query Class Interface

### 1.get_height(get height) 
```C++
Request the 'get_height' interface from the requesting node without any parameters
For example:
http://IP:port/get_height
return:
{
    "top": "",
    "type": ""
}
```

### 2.get_balance(get address balance) 

```C++
http://IP:port/get_balance  
{
  "type":"get_balance",//protocol
  "addr": ""//base58 address
}
return:
{
    "ErrorCode": "",//Success is 0
    "ErrorMessage": "",
    "addr": "",
    "balance": "",//amount
    "type": ""
}
```

### 3.get_tx_info(Interface for obtaining transaction information)

```C++
http://IP:port/get_tx_info
{
  "type":"get_tx_info",
  "txhash":"5c315686c0f5ef4e8ad71ed323e6f48e7bf1d34aca8daf0ab4ff7e193aedd3f6"
}
return:
{
    "ErrorCode": "",
    "ErrorMessage": "",
    "blockhash": "770995a669769ecbc3e4808c725a2da0bfc478b6d5feb66fd0dbf65df9164f1b",
    "blockheight": 7323,
    "tx": "{\"time\":\"1683711737796247\",\"identity\":\"131AvquS4eGEtueQzJMPZW3RubaKmHMH64\",\"hash\":\"5c315686c0f5ef4e8ad71ed323e6  f48e7bf1d34aca8daf0ab4ff7e193aedd3f6\",\"utxo\":{\"owner\":[\"1zzF8jNBAXFTPJzhvY45zLKgQmnPLBZ93\"],\"vin\":[{\"prevOut\":  [{\"hash\":\"0ab37f8dd11a9590a0997a5026a5a96fb0457da09861c5f91ccbb9820ff397e2\"},{\"hash\":\"73bdb4f138658fa274bd9293bdad38fa4d115280b4e8bc91ff0c1173befa5918\"}],\"vinSign\":{\"sign\":\"9GCIH4UL12PkaIRJsdJkyAQnAglRQFDUoPy0opQU7aXKITpRa8OWQunK/pi9VzH1Dhv2zEGqQ9c/I03fcJHaAQ==\",\"pub\":\"MCowBQYDK2VwAyEAGrd0tg1mPKp13KOOop+jdC0IK0n+G2IMfKE7OEmf570=\"}}],\"vout\":[{\"value\":\"99999\",\"addr\":\"1KeajMdKuGgLtu7YqFJ4fFhx6zTBxQCEfe\"},{\"value\":\"499846801\",\"addr\":\"1zzF8jNBAXFTPJzhvY45zLKgQmnPLBZ93\"},{\"value\":\"53200\",\"addr\":\"VirtualBurnGas\"}],\"multiSign\":[{\"sign\":\"XAASZJPIlmuZDHt6bPYv5D3vE3v3041lALXmRVCq6J7TP96YcW6R2RO8x9iAar8WNLvX+diBhCpq7wtd8RiwBg==\",\"pub\":\"MCowBQYDK2VwAyEAGrd0tg1mPKp13KOOop+jdC0IK0n+G2IMfKE7OEmf570=\"}]},\"type\":\"Tx\",\"consensus\":8,\"txType\":1,\"verifySign\":[{\"sign\":\"oJDD44w+ryyp05DdiU4n7JpoXsQEZx8KX/HqDhCwl1DvHWY2RU2g3llcAKfrnPHJDUCROl02qGT+jf36HbWIAA==\",\"pub\":\"MCowBQYDK2VwAyEAVSADHkaJgW2IbtYRNagwMXYX/T6kkaiOP6wkuxhhoME=\"},{\"sign\":\"gSFNJA214kOfyACjt7w0zgaj2oQm6i6W9TOg3hlzuVNc9RjbzXV/4GBsFtCWIWv0fJ9Y4A8JGfubsfDe4E01Aw==\",\"pub\":\"MCowBQYDK2VwAyEAVqYAdjh/93fGxbqsfGIah4/mX6DXdvOC54FoBdkNwWw=\"},{\"sign\":\"WDDVdLtPSeggjOF5XEg7cKHZ3p2ewrW5XtHbJKeQZW/V32aknaxaEd2JEgibGSg/1mhUuW09gWl+stEVTRe3AQ==\",\"pub\":\"MCowBQYDK2VwAyEAL37lf8ON71YQUbDvPhr7ndUJQ4yR+K4BFUgf9oM7rrY=\"},{\"sign\":\"7Z2I8mKxKEv4v5Msypg7mg4RXkjqXLL/ctUuzZWdcdhhKfcSG+/JlsbqM3C6P7+aRFntWIVFaAIDMtboeUzkAw==\",\"pub\":\"MCowBQYDK2VwAyEAbIgKCkKqj/dAcj96SlePfceYUKF+py0V5XaJkS6dQ7Q=\"},{\"sign\":\"2iJgSt6RCOydZR3QrSC4KDCuumqPdLZaPyQt0/2rVDScybDgDAcHWKibxLv/aEUqEVHrsgZlg6ScGHuCv2mUDg==\",\"pub\":\"MCowBQYDK2VwAyEAHyeMZNU96z/pG5Ez3/Xf1byjZCU3l3qyyIhn0udYCP4=\"},{\"sign\":\"8KeTjwsjeo63Se/ufRvLLsGSljn0MCBOEEg6qmRJIrph41iRK2vtC7TSemxtSlEmANCk0qN5ouyQW+qnhZdLAw==\",\"pub\":\"MCowBQYDK2VwAyEAR/TYtUUzIy5n7aG4P22GzOI2baHeUDJD4gqw+f0W0jo=\"},{\"sign\":\"hZUD132JsouzNa9FIFBzgat2bjj2+QJdecCKAI35WycqW+uy6Uy72QZ1RlmWNl4OkQX0oRzy21X98zNa0PTrAA==\",\"pub\":\"MCowBQYDK2VwAyEA0Fz7U6rWtvU9F3bDsBiMT91R2xp4PdUAtE4z16g1T+c=\"},{\"sign\":\"9URZUuG5e3ziRKxjCytJ5v/0Hn8PVoAfYFUEOVRnBvArSD5HihYvFAzoD1IG1TZrqlXI7RFNw/AVqFxhvWxIBQ==\",\"pub\":\"MCowBQYDK2VwAyEA6Q29AUyYeTu4FBg7KRisz8J+mH6ycU+QEZa6ZnP/ZGY=\"}]}",
    "type": ""
}
Note: The data type returned by the interface is in JSON format
```
### 4.**get_block** interface

This interface is an RPC interface, and the request parameters are as follows:

1.Parameter
top(Starting height)
num(Number of traversal heights starting from top)

2.Call Example

`http://IP:port/get_block?top=10&num=20`

return as follows:

```C+
    {
        "block":{//block
            "hash":"18dfcf300540bd04d26c118d1d52f9393b44592ecb865528afb92ffbc46dd48f",//block hash
            "height":10,//block height
            "time":1680254879190916//block time
        },
        "tx":[//Transaction body
            {
                "Consensus":8,//Number of transaction consensus
                "Cost":0,//Transaction packaging cost
                "Gas":0,//gas fee
                "Type":"Tx",//Large types of transactions, currently only the main transaction
                "identity":"127AKiaP7DTfaNiUaSAgLu66FcZCYYVLvY",//Transaction Packer
                "time":1680254875731987,//Transaction Time
                "txHash":"3a97c7b4ece389c7b5043f1d1c7aa2e173100c21e9f8f4b1c24cab1b480b3614",//Transaction hash
                "txType":1,//Small types of transactions: ordinary transactions, pledges, investments, etc.
                "utxo":{
                    "multisign":[
                        {
                            "pub":"xJMwFzmD+qN+X5lYxz30/ZQlvKqITqUpubMTNrhtbbqMX1QJjv4JlgLp2FuzdpvQEWmM4qhIksqdzck0PAQkAQ==",
                            "sign":"xJMwFzmD+qN+X5lYxz30/ZQlvKqITqUpubMTNrhtbbqMX1QJjv4JlgLp2FuzdpvQEWmM4qhIksqdzck0PAQkAQ=="
       }
                    ],
                    "owner":[
                        "157XxCrhoSZ62YKykxhPa38BogExCwxxvn"//The initiator of the transaction
                        ],
                    "vin":{
                        "prevout":{
                            "hash":[
                                "561925ff253dcae91b6bd55001d0bf6f10657082c2dc175ab08c03c4ca4b4b6d"//used utxo
                            ]
                        },
                        "vinsign":[
                            {
                                 "pub":"MCowBQYDK2VwAyEACkFeTyQOZGETJFm3NXnIK9XGDrPOVa8gdNhUYaPRuh0=",//Public key for vin signature in base64 format
                                 "sign":"e2U/6RpXQJbCVScqV1SVg7czcWXMC+a7yVt+Z7JzFKDc1p4ym/ZkLzkTbgsJTaHLK7JzECM4beyYpzCIjtRfBA=="//Information on vin signature in base64 format                          
}
                        ]
                    },
                    "vout":[
                        {
                    "addr":"1E5GEcuipacDnrrstY4xkih5sBYfacwmTh",//Transaction receiver  
                     "value":100000000//Amount received by the receiver
                        },
                        {
                            "addr":"157XxCrhoSZ62YKykxhPa38BogExCwxxvn",
                            "value":73969459600
                        },
                        {
                            "addr":"VirtualBurnGas",//burn the address
                            "value":20200//burn the amount
                        }
                    ]
                },
                "verifySign":[
                    {
                        "pub":"MCowBQYDK2VwAyEAcgX+Tp6PyrEYMA2Kn1wsvbJcUJzt4/JvBLBp0rzec10=",//Signer's public key
                        "sign":"mx3rg+Zf35yQnsTr4qOa9zYef94jEy9CBNTlG9hH93ZZviR/J5r5To6LPSJtCfD0T8kVsjc9OvnsJTMjokl6Ag==",//Signature information of the signer
                    "signaddr":"127AKiaP7DTfaNiUaSAgLu66FcZCYYVLvY"//Signer's base58
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEApFoqoHUjXmh5LWzT8LInB/uyjAgTALdS/xxc9DQEZN4=",
                        "sign":"GZDaoFMBSc9KgKDmMciUJz8KPu/pyZ3do+P56Syih3Zcmjz5y6eZ+9oASOFR1sgiUNilZCBDqGLyods8qIzECg==",
                        "signaddr":"16rk424JYwsBeHiigiQXBwhzyGsHjC5qUx"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEA3Z26vzI+gcPqhQJ52XRDgT8uPooIYeXn15HJT0ejB8U=",
                        "sign":"ZTJLMZKfVD722R2EHmcmQU8ibC3l5+xbpSb2stpRsYFZtnnoa2JMZJZf9l6g1hbH9z/7yCwXvIQ59hRb8XDjCA==",
                        "signaddr":"16mGAbCN8aZ61MBWqj65JnuuUMz3XwFhvk"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEAQYklNAOAKvgiZCpjqiHaAJ5TQ8xK4054H2LGQUbyLRI=",
                        "sign":"W2KtfpA22BZlbYzX6/oE8t16cgye1JfuWwP41EFW/N104oADTkbaFkj8xAISeZ9EYHw0y3WCvxbKQDNhG/XlDQ==",
                        "signaddr":"1GtTw5rpFjtxDMS7UAbejnVBHF9qPijpj7"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEAj2L9HbLfQHUUtsY9tku/QH36zhIG69W5Gg+zVIKf20A=",
                        "sign":"29YbwkvfKOd7KaNrxoqxaeLV5ieIbxRm2Kx3zjtbpgsHZ7+lqsq9bUsa/UOxQ5yERFe56GnolF2S5w1joEqhAQ==",
                        "signaddr":"1HwQJd6eo3X9kSgwTcbj37JSc3YaYcm5FV"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEAAU3jnfVhy+Bqf6LWKIzLU96SQsv04n3QPrs+b8SklmQ=",
                        "sign":"d+r2pLNLRvBWms4f/QGK6C0iTHaYLI9/Q4fPR5ggh3XOt2QM9hvTkUSFpZ9MusFmyOelhA3jrYT69NBu53iBBg==",
                        "signaddr":"1GVmxduCHqzi6Ebxazy1xNMCFAkjHJHBz3"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEAs3LkwwNG6Ej77oxv8qS8KlCtvw6C4M8H4rldQiq4A/4=",
                        "sign":"pPJb+5tMFmQdNGxxFfrHiSF43HgWAjpWVhH+vnRX6+YDq17AcG4yW3i1IZJacDyZtDaTbCT1D5UG+trxMSeVAQ==",
                        "signaddr":"18MBP2QMp9wsxJmHu9CKGxMnofTFAhcngw"
                    },
                    {
                        "pub":"MCowBQYDK2VwAyEApS6VOfVLV3bCeanR35FZW/i129wd1XFNFA1YaRJlNXY=",
                        "sign":"m556KFsIYy+rWCX0SHdeV6EGQqSnlrf+AECre35+oEtu6vgtwaseuwbWiAkrwlpkD+8IKNMjjNmzWeKV0MokCQ==",
                        "signaddr":"13qCpfVgU5MhfCUTLKfBFCufi71hP44dt3"
                    }
                ]
            }
        ]
    }
    
```

### 5.info interface(Return data in non JSON format)

```C++
View the status of node links
http://IP:41517/info

return:
queue:
queue_read:0
queue_work:0
queue_write:0


amount:
addr:0


Public PeerNode size is: 0

------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------
PeerNode size is: 0
```

## Transaction interface

### Prerequisite

A private key needs to be prepared to be imported for transaction signing, and an interface for importing the private key is also provided in the library.
```C++
  /*Export base64 private key*/
  __declspec(dllexport)  char * __stdcall export_new_prikey_base64();
  /*Import base64 private key handler*/
  __declspec(dllexport)  long long __stdcall import_base64_prikey_handler(const char *buf, int buf_size);
  /*Import hexadecimal private key*/
  __declspec(dllexport)  long long __stdcall import_prikey_handler_from_hex(const char *str);
```

### Transaction Process

Note: Multiple protocols are defined in this SDK
1.Get parameters: Before starting a transaction, it is necessary to obtain certain necessary parameters for the transaction (such as utxo, transaction hash, etc.) through a specified protocol
For example:

### Get stakeutxo

```C++
{
    "type":"get_stakeutxo_req",
    "fromAddr":"" //Need to obtain the account's base58
}

{
    "type":"get_stakeutxo_ack",
    "utxos":[{
        "utxo":"",//the returned stake utxo
        "value":""//the returned stake amount
    }]
}

```

### Get invested utxo
```C++
    {
        "type":"get_disinvestutxo_req",
        "fromAddr":"",//Need to obtain the account's base58
        "toAddr":""//The base58 invested by this account    
    }
    {
        "type":"get_disinvestutxo_ack"
        "utxos":[""]//Returned investment in toAddr's utxo    
    }

```

### Get Deployers
```C++
{
    "type":"deployers_req"
}

{
    "type":"deployers_ack",
    "deployers":[""]//deployers
}

```

### Get utxo for contract deployment

```C++
    {
        "type":"deploy_utxo_req",
        "addr":""//Deploying the contractor's base58
    }
    {
        "type":"deploy_utxo_ack"
        "utxos":[""]//The contract deployment utxo returned by the interface
    }

```

2.Fill in protocol:Then fill in the corresponding parameters in the protocol, form the protocol into JSON, and send it to the agency node through HTTP (as described in the transaction introduction title)
3.Node processing: The node generates a transaction, and then the transaction body will be returned through the HTTP interface
4.Transaction signature: After receiving the transaction body returned by the node, the user will sign the transaction with the content to be returned through the interface provided in librpc.dll/librpc.so.
5.Transaction uplink: At this point, the transaction has been generated and broadcasted through the HTTP interface. The result of whether the transaction was successful is then returned through the HTTP interface.

### Ordinary transactions

 ```C++
{
    "type":"tx_req",//Protocol Name
        "fromAddr":"", //Initiator's base58
        "toAddr":[{//Receiver's base58
        "addr":"",//Receiver's address
        "value":""//Amount to be transferred
    }]
}
 ```

 ### Stake Transaction

 ```C++
 {
    "type":"get_stake_req",//Protocol Name
    "fromAddr":"",//Initiator's base58
    "stake_amount":"",//stake amount
    "PledgeType":""//Pledge Type(Default to 0)
 }

 ```

### Unstake

  ```C++
  {
    "type":"get_unstake_req",
    "fromAddr":"",//Initiator of unstake transaction
    "utxo_hash":""//UTXO that needs to be unstaked(This utxo is the returned account stake through get_ stakeutxo_req interface )
  }

  ```

### Invest

  ```C++
  {
        "type":"get_invest_req",
        "fromAddr":"",//Transaction initiation
        "toAddr":"",//Investee
        "invest_amount":"",//invest amount
        "investType":""//investType(default to 0)
  }
  ```

### disinvest

  ```C++
  {
    "type":"get_disinvest_req",
    "fromAddr":"",//the initiator of disinvestment transactions
    "toAddr":"",//Investee
    "utxo_hash":""//The invested utxo(This utxo is returned through get_ disinvestutxo_ req??
  }
  ```

### Application

  ```C++
  {
    "type":"get_bonus_req",
    "Addr":""//Address for initiating the application transaction
  }

  ```

### Deployment Contract
  ```C++
  {
    "type":"contract_info",//Contract information, defined by the user
    "name":"",
    "language":"",
    "languageVersion":"",
    "standard":"",
    "logo":"",
    "source":"",
    "ABI":"",
    "userDoc":"",
    "developerDoc":"",
    "compilerVersion":"",
    "compilerOptions":"",
    "srcMap":"",
    "srcMapRuntime":"",
    "metadata":"",
    "other":""

  }
  {
    "type":"deploy_contract_req",//Deployment Contract
    "addr":"",//Deployed address
    "nContractType":"",//Contract Type??default to 0??
    "info":"",//
    "contract":"",//generated contract
    "data":"",//constructors�� parameters
    "pubstr":""//Public key after base64
  }

  ```

### Execute Contract

  ```C++
  {
    "type":"call_contract_req",
    "addr":"",//Address for executing the contract
    "deployer":"",//deployer
    "deployutxo":"",//Deploying utxo for contracts
    "args":"",//Contract parameters
    "pubstr":""//Public key after base64
  }

  ```



## Callback the interface

1.Enable and set the interface parameters for config.json
   In config.json, modify 'http_callback' parameter ,the meanings are as follows:
    ip: callback IP address
   path: callback path
   port: callback port


2. The node will make RPC calls based on the following callback path composed of the above three items
```C++
http://ip:port/path/add_block  // add block callback
http://ip:port/path/rollback_block // rollback block callback
```
Adding blocks or rolling back are both blocks, so the callback data is JSON's block data.
Callback example:
```C++
{
    "hash": "ebf4c94a8854a13aba699698106af58ed74e5ba36e2943abcc6a341f79761180",//block hash
    "height": 1571,//block height
    "time": 1680497838594417,//block time 
    "tx": [
        {
            "data": {
                "BonusAddrList": 6,
                "BonusAmount": 23287671232// the bonus amount            
                },
            "from": [
                "17rkWgWpiSoKMdooMRvap84p6Wr2v2pc7b"//initiator of trasaction
                ],
            "hash": "63634c89ef484330efa19175cc589fce3f336d084784c2ad2c1041eec586dcc2",//transaction hash
            "time": 1680497838065903,//transaction time
            "to": [
                {
                    "pub": "17rkWgWpiSoKMdooMRvap84p6Wr2v2pc7b",//the receiver of transaction
                    "value": 1885369863// the amount received by the receiver 
                },
                {
                    "pub": "1CtuZNLKCwSEiWXbcG85426RQbA2jgaspQ",
                    "value": 4508493150
                },
                {
                    "pub": "1Dogspn7FrGnJqbx63B2TJZkhDCxqMZBk6",
                    "value": 2147682192
                },
                {
                    "pub": "1NKt8KNqsYqKQTNoEFX5SaSWb6nVtzmhBA",
                    "value": 11951605479
                },
                {
                    "pub": "17rkWgWpiSoKMdooMRvap84p6Wr2v2pc7b",
                    "value": 11346438396
                },
                {
                    "pub": "VirtualBurnGas",// burn the address
                    "value": 36000//burn the value                
                }
            ],
            "type": 99//transaction type??details are as follows
        }
    ]
}

```

3.Transaction Types

   -1: The foundation block
   0: unknown
   1: Ordinary transaction
   2: Staking transaction 
   3: Unstaking transaction
   4: Invest transaction 
   5: Disinvest transaction 
   6: Unchanged
   7: Deploy contract
   8: Execute contract 
   99:Apply for bonus
