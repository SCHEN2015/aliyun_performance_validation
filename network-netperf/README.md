# aliyun_performance_validation

Performance Validation on Alibaba Cloud with Ansible

# Usage

## Ping all the hosts
ansible all -m ping -o

## Install test tools
ansible-playbook ./install_netperf.yml

## Optimization before testing
ansible-playbook ./performance_optimize.yml

## Check the status of the hosts
ansible all -m script -a "./scripts/check_environment.sh"

## Copy the private key to test host (for test script to run)
ansible test -m copy -a "src='~/.pem/cheshi-docker.pem' dest='/root/sshkey.pem' mode=400"

## Get a list of peer-ips
ansible peers -m shell -a "ifconfig eth0 | grep inet | awk '{print \$2}'" | grep 172 | xargs echo
ipaddrs=$(ansible peers -m shell -a "ifconfig eth0 | grep inet | awk '{print \$2}'" | grep 172 | xargs echo)

## Run the test scripts
ansible test -m script -a "./scripts/netperf_test.sh <peer-ip list>"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs $ipaddrs"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs $ipaddrs $ipaddrs $ipaddrs"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs"
ansible test -m script -a "./scripts/netperf_test.sh $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs $ipaddrs"


## Check the log
ansible test -m command -a 'ls netperf_test_*.log'

