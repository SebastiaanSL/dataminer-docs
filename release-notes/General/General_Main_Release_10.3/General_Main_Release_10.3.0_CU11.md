---
uid: General_Main_Release_10.3.0_CU11
---

# General Main Release 10.3.0 CU11 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### SNMPv3 responses now have a dynamic size [ID_37948]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

Up to now, the size of SNMPv3 responses was limited to 16000 bytes. When larger responses were received, a timeout message would appear in StreamViewer.

From now on, the size of SNMPv3 responses will no longer be limited, meaning that the only constriction will be the maximum size of a UDP packet (i.e. 65000 bytes).

> [!NOTE]
> When sending SNMPv3 messages, the size of those messages is still limited to 16000 bytes.

#### Enhanced performance when compiling QActions in SLScripting [ID_37993]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When QActions are compiled in SLScripting, several resources need to be loaded. Up to now, those resources would be loaded for every QAction individually. From now on, they will be loaded only once and stored in a cache in order to reduce memory and CPU overhead.

Every 10 seconds, resources that have not been referenced in the last 30 seconds will be removed from the cache.

> [!NOTE]
> Uploading protocol or app packages that contain different versions of DLL files stored in the same location may not compile against the shipped version if the previous version was also uploaded and put in use in the previous 60 seconds. Forcing a recompilation of the QActions a minute later (causing the packages to be uploaded again) will yield the expected result.
>
> Protocols and scripts should use NuGet packages as much as possible. The DLL files in those packages will then automatically be placed in folders by version. When protocols use custom non-NuGet DLL files, those should also be placed in folders by version.
>
> With DLL files such as NewtonSoft, which protocols do not reference using NuGet, overwriting the DLL file with a newer version will cause protocols with QActions that have already been compiled to no longer work after a DataMiner restart as the correct strong-named assembly can no longer be found.

#### Elasticsearch/OpenSearch: TTL-based rollover for the CustomData and LoggerTables storage types is now disabled [ID_38000]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

TTL-based rollover for the CustomData and LoggerTables storage types is now disabled.

#### Security enhancements [ID_38040]

<!-- 38040: MR 10.3.0 [CU11] - FR 10.4.2 -->

A number of security enhancements have been made.

#### NATS: All nodes will now be considered primary nodes [ID_38089]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

From now on, there will no longer be any primary and secondary NAS configurations. All nodes will now be considered primary and will be using their local credential files.

Also, when the NATS configuration is reset, the DMS IP addresses will now be collected via the online Failover agent.

### Fixes

#### SLDataGateway: Problem with casing when retrieving data from Elasticsearch/OpenSearch [ID_37835]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When SLDataGateway retrieved data from Elasticsearch/OpenSearch on behalf of a DataMiner app (e.g. Ticketing), in some cases, it would pass an incorrect result set to that app due to a casing issue.

#### Security: Users would incorrectly not be allowed to update the Visio file linked to a service [ID_37866]

<!-- MR 10.3.0 [CU11] - FR 10.4.1 -->

Up to now, when users had the following permissions, they would not be allowed to update the Visio file associated with a service by using the *Upload new visio file* or *Set new blank visio file* commands:

- *General > Visual Overview > Access Visual Overviews*
- *General > Visual Overview > Edit Visio drawings*
- *General > Services > Edit*
- *Write* and *Config* permission for the service in question

From now on, when users have the permission to link a Visio file to a specific service, they will always be allowed to update the Visio file linked to that service.

#### Service & Resource Management: Timeout script in end event of booking would not get executed when the booking was set to end while the DMA was being stopped [ID_37911]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When the end event of a booking used a timeout script, in some cases, that script would not get executed when the booking was set to end while the DataMiner Agent was being stopped.

#### DataMiner Taskbar Utility: Problem when making SLTaskbarUtility perform an action using the command prompt [ID_37952]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When you made the DataMiner Taskbar Utility perform some action using the command prompt, the arguments would not be parsed correctly when no instance of SLTaskbarUtility was running.

#### GQI: 'Could not find PK column' error after performing a query against an empty parameter table [ID_37978]

<!-- MR 10.3.0 [CU11] - FR 10.4.1 -->

Up to now, in some rare cases, performing a GQI query against an empty parameter table would result in a `Could not find PK column` error. From now on, GQI will return an empty result set instead.

#### SLDataGateway would incorrectly keep waiting for acknowledgements from SLDataGatewayAPI [ID_37985]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

SLDataGateway would incorrectly keep waiting for an acknowledgement from SLDataGatewayAPI, causing numerous `Waiting for SLDataGatewayAPI to acknowledge ...` entries to be added to the *SLDataGateway.txt* log file.

#### Problem with SLProtocol when a parameter was updated while an SLA window was changing [ID_37990]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When one of the following parameters was updated while an SLA window was changing, a run-time error could occur in SLProtocol:

- Base timestamp
- Monitor span
- Window size
- Window unit
- Window type
- Validity start
- Validity end

#### SLNet: Problem when a client application sent multiple messages to the same manager [ID_38025]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When a client application (e.g. DataMiner Cube) sent multiple messages to the same manager, in some cases, a number of those messages would return an exception and would not get processed.

#### Problem with protocol compliancies cache in SLNet [ID_38043]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

The compliancies cache in SLNet, which keeps track of the minimum required version of a protocol or of whether a protocol supports Cassandra, was only refreshed when you uploaded a *protocol.xml* file that did not contain a `<Compliancies>` tag or when the cache was accessed for the first time.

#### GQI: Problem when retrieving a large amount of alarms [ID_38065]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When a GQI query had to retrieve a large amount of paged alarms, after a while, a timeout exception would be thrown even though none of the paged requests had timed out.