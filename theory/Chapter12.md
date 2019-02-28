# 12장 이더리움

## 이더리움 이란?

- 2015년 출시된 차세대 스마트 계약 분산 응용프로그램 기술, 스위스를 거점으로 하는 Ethereum Foundation에서 개발이 진행되고 있는 오픈소스 프로젝트이다.
- 이더리움은 Solidity등의 튜링완전성(Turing-Completeness)을 갖춘 확장용 언어를 갖춰 스마트 계약을 쉽고 간단하게 프로그램을 만들 수 있다.
- 합의알고리즘으로 PoW를 채택하고 있지만 앞으로는 PoS로 변경하는 것을 검토하고 있다.
- 이더리움은 가상화폐로 Ether라는 단위를 사용한다.
- 물론 Ether보다 더 작은단위로 10^-8 Ether = Szabo, 10^-18 = Wei라는 단어를 사용한다.
- 비트코인과 이더리움은 p2p 네트워크 상에서 거래 이력을 블록체인에 기록하는 반면 비트코인과 다르게 스마트 계약 그 자체나 실행 이력도 기록할 수 있는 특징이 있다.
- 비트코인과 마찬가지로 블록이 생성되면 블록에 저장된 스마트 계약이나 송금이 실행된다.
- 스마트 계약이나 송금 이력은 블록에 저장되므로 그 기록은 정당성을 가지게 된다.
- 스마트 계약의 실행환경은 EVM(Ethereum Virtual Machine) 이라 하며 이더리움 클라이언트 소프트웨어에 포함되어 있다.
- Solidity로 작성된 Contract는 EVM에서 동작하기 때문에 자바 가상 머신과 마찬가지로 운영체제에 종속되지 않는다.
- 최근에는 IoT분야에도 적용하기위해 라즈베리파이용 바이너리 코드도 제공하고 있다.
- Ethereum Client는 C++, Go, Python등 많은 언어로 구현돼 있지만 Go 언아판이 가장 활발하게 되어있다.
- 이더리움에는 기본 기능으로 비트코인과 같은 화폐기능이 있다.


## 이더리움 설치
- 이더리움은 가장 업데이트 빈도가 높은 Go 언어로 개발된 Go-Ethereum(이후 geth)를 이용한다.
- apt-get으로 설치할 수 있지만 업데이트 빈도가 높기때문에 기존 코드가 작동하지 않을 수 있다. 때문에 git 에서 소스코드를 받아 빌드하는것을 추천한다.

``` bash
mkdir Workspace
cd Workspace

# go-ethereum 소스코드 설치
git clone -b release/1.3.6 https://github.com/ethereum/go-ethereum.git

# go 환경 설치
sudo apt-get install -y build-essential libgmp3-dev golang

# geth 빌드
make -C go-ethereum geth

# 버전 확인
./go-ethereum/build/bin/geth version

# 명령어로 실행 가능 하도록 path 추가
sudo cp ./go-ethereum/build/bin/geth /usr/bin
```

## 테스트 네트워크 구축

``` bash
cd Workspace
mkdir eth_data
cd eth_data

geth --networkid "123" --datadir "eth_data" --olympic console

# geth --networkid [네트워크 식별자]
#      --datadir [워크 파일이 저장될 디렉토리]
#      --olympic [테스트 네트워크 사용]
#      console [콘솔 모드로 기동]
```

#





