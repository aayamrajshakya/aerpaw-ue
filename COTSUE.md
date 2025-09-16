# Cots UE for AERPAW (exploring alternatives)

> :exclamation: We have to run the following two programming commands before we run the Open5GS container

## Opencells SIM programming

```bash
sudo ./program_uicc --adm 11405625 --imsi 001010000088516  --isdn 00000001 --acc 0040 --key 8EAE4E0E5BFAC60B65E192581234D02A --opc 9CA4C48F83E123270B66E31FF68FB289 -spn "OpenAirInterface" --authenticate
```

## Pysim SIM programming

```bash
./pySim-prog.py -p0 -s 8988211000000885163 -x 001 -y 01 -a 11405625 --imsi=001010000088516 --opc=9CA4C48F83E123270B66E31FF68FB289 --msisdn=00000001 --acc 0040 -k 8EAE4E0E5BFAC60B65E192581234D02A -n "OpenAirInterface"
```

## Check for the `dnn` parameter in Open5GS config file:

> Config filepath: `/opt/open5gs/build/configs/open5gs_nr_core_oai.yaml`

Look for the `dnn` parameter under SMF & UPF, which should match with the `APN` of the SIM card.

<img title="" src="file:///home/aerpaw-msu/mdmanual/apn.png" alt="apn.png" width="271" data-align="center">

> :warning: Make sure both the name and APN are exactly the same

# How to run

## 1) Start the docker container:

```bash
sudo docker run -it --privileged -v /dev/bus/usb:/dev/bus/usb --net host --cap-add=NET_ADMIN --cap-add=SYS_NICE 7ea939d733c6 /bin/bash
```

## 2) Initiate a TMUX session and start Open5GS:

```bash
cd ~/Profiles/ProfileScripts/Radio/Helpers
./startOpen5GS.sh /opt/open5gs/build/configs/open5gs_nr_core_oai.yaml
```

## 3) Add SIM parameters to the Open5GS database:

```bash
/opt/open5gs/build/misc/db/open5gs-dbctl add 001010000088516 8EAE4E0E5BFAC60B65E192581234D02A 9CA4C48F83E123270B66E31FF68FB289
```

## 4) Open a second TMUX session and start gNB:

```bash
cd ~/Profiles/ProfileScripts/Radio/Helpers
export LAUNCH_MODE=TESTBED
./start_OAI_gNB.sh
```

## 5) Run an iPerf test:

For the purpose of testing, we used the following apps:

<img title="title-1" src="file:///home/aerpaw-msu/mdmanual/app2.png" alt="alt-text-1" width="320"> <img title="title-2" src="file:///home/aerpaw-msu/mdmanual/app1.png" alt="alt-text-2" width="325">



### Traffic results:

<img title="ping" src="file:///home/aerpaw-msu/mdmanual/ping.png" alt="ping" width="322"> <img title="iperf" src="file:///home/aerpaw-msu/mdmanual/iperf.png" alt="iperf" width="323">
