# 11장 Bitcoin Core

## 작업순서

1. Bitcoin Core 설치
2. 테스트넷에서 Bitcoin Core 기동
3. Bitcoin Core 계정 생성
4. Bitcoin Core 송금
5. Bitcoin Core에서의 채굴
6. 트랜젝션과 블록 내용 확인

## 환경

Parallels + ubuntu 16.04

## 설치 get started

``` bash

# 작업환경 생성
mkdir bitcoin-core
mkdir bitcoin-core/src
cd bitcoin-core/src
git clone https://github.com/bitcoin/bitcoin.git

sudo apt-get update

# gcc 설치
sudo apt-get install build-essential automake pkg-config libevent-dev bsdmainutils -y

# Open SSL
sudo apt-get install libtool autotools-dev autoconf libssl-dev -y

# Boost
sudo apt-get install libboost-all-dev -y

# libdb4.8
sudo apt-get-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev -y

# 관련 라이브러리 설치
sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler -y


# 빌드
cd bitcoin
./autogen.sh
./configure
make
sudo make install
서 
```

## 테스트넷 기동 
비트코인에는 2개의 테스트 모드가 있다.

- **Testnet:** 인터넷상에서 동작하는 테스트 네트워크, 테스트용 BTC를 사용하지만 이미 대량의 블록체인이 존재하고 있기 때문에 처음 시작할 때 모든 데이터를 취득해야 한다.

- **Regtest:** 로컬 PC 내에서의 테스트 네트워크. 자유롭게 계정을 만들거나 채굴할 수 있으며 블록체인 초기화도 쉽기 때문에 시험용으로 사용하기에 적절하다.

- bitcoind 기동

``` bash
bitcoind -regtest -daemon
# bitcoind가 실행 상태가 되므로 다른 터미널에서 bitcoin-cli를 사용해 비트코인을 조작해야 한다.
```

## Bitcoin Core조작

- bitcoind까지 실행이 됐다면 송금을 하기 위한 BTC를 생성한다. 비트코인은 블록을 생성한 보상으로 BTC를 받을 수 있다.
- 비트코인은 보상을 받은 후 100블록이 경과하지 않으면 송금 등을 이용할 수 없기 때문에 101개의 불록을 만든다.

#### 비트코인 블록 생성

``` bash
bitcoin-cli -regtest generate 101
```

#### 블록 수 확인

``` bash
bitcoin-cli -regtest getblockcount
```

#### 계좌 생성

``` bash
bitcoin-cli -regtest getnewaddress testuser1
# 생성되는 결과값은 잘 저장해야 한다.
```

#### 잔고 확인

``` bash
bitcoin-cli -regtest getbalance
```

#### 특정 계좌의 잔고 확인

``` bash
bitcoin-cli -regtest getbalance testuser1
```

#### 송금

``` bash
bitcoin-cli -regtest sendtoaddress {계좌주소} 10 
# {계좌주소}로 10 비트코인을 전송
```

#### 트랜젝션(송금) 내역 확인

``` bash
bitcoin-cli -regtest listunspent
# 확정된 트랜젝션 확인
bitcoin-cli -regtest listunspent 0
# 0을 추가하면 미확정 트랜젝션을 확인 할 수 있다.
```

#### 통장잔고 확인

``` bash
bitcoin-cli -regtest getbalance
# 송금액은 아직 전달되지 않았지만 수수로가 먼저 차감되어 있을것이다. 블록체인에서는 트랜잭션을 발행한 것만으로는 송금이 확정되지 않는다. 이후 실행하는 채굴에 의해 송금이 확정된다.
```

#### 채굴

``` bash
bitcoin-cli -regtest generate 1
# 블록체인에서는 채굴에 의해 트랜젝션이 블록에 저장되고, 트렌젝션이 블록에 저장돼야 송금이 확정된다.
```

#### 송금 확인

``` bash
bitcoin-cli -regtest listunspent
# 채굴을 하였기 때문에 블록이 생성되었고 트랜젝션이 미확정에서 확정으로 변했다. 그러므로 0 인자를 추가하지 않아도 결과가 나타날 것이다.
```

#### testuser1의 잔고 확인

``` bash
bitcoin-cli -regtest getbalance testuser1
```


















