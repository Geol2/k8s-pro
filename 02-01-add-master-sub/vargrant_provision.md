# 호스트 전용 설정

DHCP 설정 자동 설정 추가

```shell
vagrant ssh
```

```shell
sudo vi /etc/resolv.conf
```

```shell
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
echo "nameserver 8.8.4.4" | sudo tee -a /etc/resolv.conf
```

```shell
sudo vi /etc/yum.repos.d/CentOS-Base.repo
```

위 명령어를 통해서 추가하던가 아래와 같이 터미널에 바로 추가한다

```shell
sudo sed -i 's/mirrorlist=/#mirrorlist=/g' /etc/yum.repos.d/CentOS-Base.repo
sudo sed -i 's/#baseurl=http:\/\/mirror.centos.org/baseurl=http:\/\/vault.centos.org/g' /etc/yum.repos.d/CentOS-Base.repo
```

```shell
config.vm.provider "virtualbox" do |vb|
  vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
```
각 전체 노드와 마스터인

`vagrant ssh m-k8s`, `vagrant ssh w1-k8s`, `vagrant ssh w2-k8s`, `vagrant ssh w3-k8s` 에서

`epel` / 추가 구성됨을 확인한다

`vi .bashrc` 에서 문법 하이라이트 적용 확인

-----

```shell
chmod +x ping_2_nds.sh
```

핑테스트 시, 다음과 같이 명령어 설정 추가