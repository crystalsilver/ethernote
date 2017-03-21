![Etherenote Logo](https://github.com/blocknotary/ethernote/raw/master/design/logo.png)

[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/hyperium/hyper/master/LICENSE)

## Installation

1. Download zip archive
2. Unpack it
3. Go to the root folder in terminal install the dependencies `npm install`
4. Set **environment** in web/config.json (see config.json with placeholders below): `dev` or `live`
5. Set **useGlobalToken** `false`
6. Set **helloSignKey** with your HelloSign API key. HelloSign is used to sign agreements.
7. Set **mongodbConnectionString** with your mongoDB connection string. MongoDB is used to store logic of EtherNote application.
8. Set **hashSalt** with string of letters and digits. It will be used as a salt for hash creating from agreement data base64 string.
9. Set **AWS** credentials:

   **host** - AWS S3 endpoint. For example, "s3.amazonaws.com".
   
   **bucket** - AWS S3 bucket name
   
   **region** - AWS region. For example, "us-east-1" (Check available [AWS S3 regions](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region))
   
   **secretAccessKey** - AWS secretAccessKey
   
   **accessKeyId** - AWS accessKeyId
10. Launch any Ethereum RPC client. For example, [testrpc](https://github.com/ethereumjs/testrpc)
11. Set **Ethereum** config:
   
      **rpc** - Ethereum RPC client url (`http://host:port`). If client is started on the same host at default port: `http://localhost:8545`
   
      **user** - Ethereum RPC client url basic HTTP auth username
   
      **pass** - Ethereum RPC client url basic HTTP auth password
   
      remove **user**, **pass** parameters from config, if an access to Ethereum RPC client url is anonymous
      
      **acc** - Ethereum account address, where contract will be deployed
   
12. Go to the root folder in terminal `/` and run `node deployContract.js` to deploy your smart contract into Ethereum.
13. After creation you will get the message in terminal like this:
    *Contract mined! address:* **0xb713e9195f44a10383015f38774f31869053750c** *transactionHash: 0x85e85f78a4e1b40f26e491eb88b9a231b31085db11799734edc54d0285edc190*
14. Copy created smart contract address from this message and paste it to the config.json to `contractAddress.dev` or `contractAddress.live` depending on your environment.
15. Go to the root folder in terminal and start EtherNote web application `node app`

### 
config.json with placeholders
```
{
    "environment": "live/dev",
    "useGlobalToken": false,
    "globalToken": "globalToken_for_using_ethernote_api",
    "helloSignKey": "helloSign_key",
    "mongodbConnectionString": "mongodb://user:password@host:port/database",
    "hashSalt": "salt_for_creating_hash",
    "AWS": {
      "host": "s3.amazonaws.com",
      "bucket": "AWS_S3_bucket",
      "region": "AWS_region",
      "secretAccessKey": "AWS_secretAccessKey",
      "accessKeyId": "AWS_accessKeyId"
    },
    "Ethereum": {
      "dev": {
        "rpc": "http://host:port",
        "acc": "0x0000000000000000000000000000000000000000"
      },
      "live": {
        "rpc": "http://host:port",
        "user": "username",
        "pass": "password",
        "acc": "0x0000000000000000000000000000000000000000"
      },
      "smartContract": {
        "bin": "0x606060405260008054600160a060020a031916331790556105b5806100246000396000f3606060405236156100565760e060020a60003504632c854a1a811461005857806341c0e1b5146100fe578063824d02271461011b578063e3ac064a14610229578063e3ffc9a3146102ce578063f6a0576d146102ed575b005b6103906004808035906020019082018035906020019191908080601f016020809104026020016040519081016040528093929190818152602001838380828437509496505050505050506000600160005082604051808280519060200190808383829060006004602084601f0104600f02600301f150905001915050908152602001604051809103902060005060010160009054906101000a900460ff1690505b919050565b610056600054600160a060020a039081163390911614610412575b565b6103a46004808035906020019082018035906020019191908080601f016020809104026020016040519081016040528093929190818152602001838380828437509496505050505050506020604051908101604052806000815260200150600160005082604051808280519060200190808383829060006004602084601f0104600f02600301f15090500191505090815260200160405180910390206000506000016000508054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561044b5780601f106104205761010080835404028352916020019161044b565b6103906004808035906020019082018035906020019191908080601f016020809104026020016040519081016040528093929190818152602001838380828437509496505050505050506000600160005082604051808280519060200190808383829060006004602084601f0104600f02600301f150905001915050908152602001604051809103902060005060010160019054906101000a900460ff1690506100f9565b610056600054600160a060020a03908116339091161461045757610119565b6100566004808035906020019082018035906020019191908080601f01602080910402602001604051908101604052809392919081815260200183838082843750506040805160208835808b0135601f810183900483028401830190945283835297999860449892975091909101945090925082915084018382808284375094965050505050505060005433600160a060020a039081169116146104b2576104ae565b604080519115158252519081900360200190f35b60405180806020018281038252838181518152602001915080519060200190808383829060006004602084601f0104600f02600301f150905090810190601f1680156104045780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b600054600160a060020a0316ff5b820191906000526020600020905b81548152906001019060200180831161042e57829003601f168201915b505050505090506100f9565b60008054604051600160a060020a0391821692913016319082818181858883f15050505050565b505060208201516001919091018054604093909301516101000260ff199390931690911761ff0019169190911790555b5050565b606060405190810160405280828152602001600081526020016000815260200150600160005083604051808280519060200190808383829060006004602084601f0104600f02600301f15090500191505090815260200160405180910390206000506000820151816000016000509080519060200190828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061058157805160ff19168380011785555b5061047e9291505b808211156105b1576000815560010161056d565b82800160010185558215610565579182015b82811115610565578251826000505591602001919060010190610593565b509056",
        "abi": [{"constant":true,"inputs":[{"name":"docId","type":"string"}],"name":"getLenderPayStatusById","outputs":[{"name":"","type":"bool"}],"type":"function"},{"constant":false,"inputs":[],"name":"kill","outputs":[],"type":"function"},{"constant":true,"inputs":[{"name":"docId","type":"string"}],"name":"getDocHashById","outputs":[{"name":"","type":"string"}],"type":"function"},{"constant":true,"inputs":[{"name":"docId","type":"string"}],"name":"getBorrowerPayStatusById","outputs":[{"name":"","type":"bool"}],"type":"function"},{"constant":false,"inputs":[],"name":"sendEtherToOwner","outputs":[],"type":"function"},{"constant":false,"inputs":[{"name":"docId","type":"string"},{"name":"docHash","type":"string"}],"name":"newDoc","outputs":[],"type":"function"},{"inputs":[],"type":"constructor"}],
        "contractAddress": {
          "dev": "0x0000000000000000000000000000000000000000",
          "live": "0x0000000000000000000000000000000000000000"
        }
      }
    }
}
```
