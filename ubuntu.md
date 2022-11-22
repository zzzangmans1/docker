# 비트코인 dApp 개발

우분투 설치

docker pull ubuntu

<img width="636" alt="image" src="https://user-images.githubusercontent.com/52357235/202600821-c043cf5e-175b-4ce9-a384-504bac4d575f.png">

필요한 툴을 깔기 위해 

apt update

<img width="746" alt="image" src="https://user-images.githubusercontent.com/52357235/202601760-cd1af1b3-4595-49f2-9c44-8a062a2969b9.png">

ping을 사용하기 위해 다운로드

<img width="831" alt="image" src="https://user-images.githubusercontent.com/52357235/202601839-c08cc912-ea97-46a3-ae23-4c030ba07f03.png">

ifconfig를 사용하기 위해 다운로드

<img width="859" alt="image" src="https://user-images.githubusercontent.com/52357235/202602006-c3fb89c5-e55b-4caa-af19-c33510721552.png">

ping을 쏴서 비트코인 도커에 쏘기

<img width="1348" alt="image" src="https://user-images.githubusercontent.com/52357235/202601926-db219347-682b-4899-a9e0-a749223f035a.png">

# NODE.JS 다운로드

apt autoremove 

<img width="622" alt="image" src="https://user-images.githubusercontent.com/52357235/202603469-99275950-63d5-4d28-ba84-ccd831acca6e.png">

curl을 사용하기 위해 다운로드

<img width="863" alt="image" src="https://user-images.githubusercontent.com/52357235/202602338-ff79697f-8abf-44a5-bba8-64926f9027d7.png">

curl에서 node.js 버전 다운로드

<img width="862" alt="image" src="https://user-images.githubusercontent.com/52357235/202602808-7ae7be9a-a038-43b9-a0c4-c45d81227700.png">

node.js 다운로드

<img width="860" alt="image" src="https://user-images.githubusercontent.com/52357235/202602691-fdd9f157-a182-4c0d-8ee9-bba4a000e756.png">

node.js 버전 확인

<img width="239" alt="image" src="https://user-images.githubusercontent.com/52357235/202603568-eb65873f-5049-494b-a8a4-fc77c4d6e158.png">

npm 버전 확인

<img width="231" alt="image" src="https://user-images.githubusercontent.com/52357235/202603599-a78ceba4-d21a-4b45-83ae-c0f179c7df5a.png">

패키지 만들기

cd /root
mkdir bitcoin_dapp
cd bitcoin_dapp

패키지 초기화

<img width="632" alt="image" src="https://user-images.githubusercontent.com/52357235/202604202-f222df9b-d16a-4c9d-bc3a-fce03d6a3bf6.png">

package.json가 만들어진다.

<img width="432" alt="image" src="https://user-images.githubusercontent.com/52357235/202604271-c53c676e-5ee5-4ec0-b1a6-9a18268b7692.png">

rpc 프로토콜과 통신할 수 있는 라이브러리 다운로드

<img width="858" alt="image" src="https://user-images.githubusercontent.com/52357235/202605001-1a65e67a-12f3-4e27-ba23-a91480ba516e.png">

위 모듈을 설치하면 node-modules 가 설치되있다.

<img width="474" alt="image" src="https://user-images.githubusercontent.com/52357235/202605151-096725bd-e967-4139-9473-b6c39212f950.png">

비트코인 서버 실행 (bitcoin cantainer에서 실행)

기존 비트코인 명령어와 비슷한데 -rpcallowip 로컬 ip 아니니까 추가해줘야 한다.
0.0.0.0/0 은 모든 ip를 다 허용해준다는 뜻

<img width="851" alt="image" src="https://user-images.githubusercontent.com/52357235/202605636-92a05ebb-94dd-4ff6-94c9-0ceb426d290a.png">

기본 소스 연결
비트코인서버에서 ip a 로 아이피 확인
```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient( {
  user: "test",
  pass: "test",
  host: "172.17.0.3", 
  port: 12345

});
```

<img width="367" alt="image" src="https://user-images.githubusercontent.com/52357235/203021351-735eb538-3ee0-4ad5-9116-62c154615062.png">

<img width="791" alt="image" src="https://user-images.githubusercontent.com/52357235/203020716-e7ddd1fc-e2c0-4613-8042-fadb33e18556.png">

계정 생성
비트코인 ip를 호스트에 입력

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let createAddress = await client.getNewAddress("mung");
	console.log(createAddress);
}) ();
```

<img width="566" alt="image" src="https://user-images.githubusercontent.com/52357235/203186279-26f0bfe5-c4c7-4c79-82e3-9ab3f45ab313.png">

라벨 확인

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let labels = await client.listAccounts();
	console.log(labels);
}) ();
```

<img width="512" alt="image" src="https://user-images.githubusercontent.com/52357235/203186718-de58471f-0598-4e66-ab39-0682213f9263.png">

블록 개수 확인

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let blockNumber = await client.getBlockCount();
	console.log(blockNumber);
}) ();
```

<img width="374" alt="image" src="https://user-images.githubusercontent.com/52357235/203186915-774a2261-c8f7-4c02-bc50-73c9113daa0f.png">

블록 생성 조회

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let blockHash = await client.generate(102);
	console.log(blockHash);

	let blockNumber = await client.getBlock(blockHash.result[0]);
	console.log(blockNumber);
}) ();
```

<img width="738" alt="image" src="https://user-images.githubusercontent.com/52357235/203187328-4d5ab2b9-6891-4948-9c02-410f9eda72f8.png">

트랜잭션 발생

to에 들어갈 해시값은 위에서 계정 해시값을 넣는다.

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let to = "2MxFkJMmAjXVV3Vn2zvXbD4Wpk9AP7xntBb";
	let txHash = await client.sendToAddress(to, 5);
	let txPool = await client.getRawMemPool();
	await client.generate(1);
	console.log(txHash);
	console.log(txPool);
}) ();
```

<img width="625" alt="image" src="https://user-images.githubusercontent.com/52357235/203187980-5fee166e-0f23-488e-8825-4821b45ac57b.png">

UTXO 확인

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let UTXO = await client.listUnspent();
	console.log(UTXO);
}) ();
```

<img width="734" alt="image" src="https://user-images.githubusercontent.com/52357235/203188374-dc422388-5ae6-4646-bed1-4df30fe139aa.png">

잔액조회

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let balance = await client.getBalance();
	console.log(balance);
}) ();
```

<img width="374" alt="image" src="https://user-images.githubusercontent.com/52357235/203188530-3980caba-8288-485c-9be4-2fab85a50736.png">

move 전송

```
let RpcClient = require("bitcoind-rpc-client");
let client = new RpcClient({
	user: "test",
	pass: "test",
	host: "172.17.0.3",
	port: 12345
});

(async function() {
	let from = "";
	let to = "mung";
	let amount = 5;
	let result = await client.move(from, to, amount);
	let accounts = await client.listAccounts();
	console.log(result);
	console.log(accounts);
}) ();
```

<img width="536" alt="image" src="https://user-images.githubusercontent.com/52357235/203189152-4dad6152-0eaf-47fa-84ac-41e4ec67b462.png">
