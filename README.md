Install ganache CLI

node_modules/.bin/ganache-cli

compiler=require('solc')
eth= require('web3')
fs= require('fs')

sourceCode = fs.readFileSync("Hello.sol").toString();
compiledCode = compiler.compile(sourceCode);
helloInterface = JSON.parse(compiledCode.contracts[':Hello'].interface);
helloByteCode= compiledCode.contracts[':Hello'].bytecode

web3= new eth('http://localhost:8545')
web3.eth.getAccounts().then(function(res){accounts=res});
helloContract = new web3.eth.Contract(helloInterface);
helloContract.deploy({data:helloByteCode}).send({from: accounts[0], gas:4700}).then(function(res){myContract=res;});
