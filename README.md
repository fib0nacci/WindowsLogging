# WindowsLogging
Materials that go along with the 2018 IWS presentation. Contents of this repo:
- XML files for the subscriptions. Check out the wiki for how they work
- winlogbeats config for the WEF servers to send to Kafka
- logstash pipeline for windows logs
- windows elasticsearch index template

# WEF primer
Wef is both awesome and a turd. The awesome part is the pub-sub concepts. To set up the subscription, try this out:
1. create a windows server
2. Set up the GPO
3. load up the WEF template
```wecutil.exe cs path_to_xml_file```
4. watch the logs stream in
```Get-WinEvent -LogName ForwardedEvents -FilterHashtable @{logname='ForwardedEvents';ID=4104} -MaxEvents 10```

Should you think the WEF is broken, try this out:
1. list wef subscriptions
```wecutil.exe es```
2. check out the subscription details
```wecutil.exe gs [name_from_#1]```
3. check out the statistics
```wecutil.exe gr [name_from_#1]```
4. retry the subscription
```wecutil.exe rs [name_from_#1]```