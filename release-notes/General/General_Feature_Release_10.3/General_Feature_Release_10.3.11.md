---
uid: General_Feature_Release_10.3.11
---

# General Feature Release 10.3.11 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!IMPORTANT]
> When downgrading from DataMiner Feature Release version 10.3.8 (or higher) to DataMiner Feature Release version 10.3.4, 10.3.5, 10.3.6 or 10.3.7, an extra manual step has to be performed. For more information, see [Downgrading a DMS](xref:MOP_Downgrading_a_DMS).

> [!TIP]
>
> - For release notes related to DataMiner Cube, see [DataMiner Cube Feature Release 10.3.10](xref:Cube_Feature_Release_10.3.10).
> - For release notes related to the DataMiner web applications, see [DataMiner web apps Feature Release 10.3.10](xref:Web_apps_Feature_Release_10.3.10).
> - For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

## Highlights

*No highlights have been added to this section yet.*

## New features

*No new features have been added to this release yet.*

## Changes

### Enhancements

#### Cassandra Cluster Migrator is now able to resume a migration that was in progress when a DMA was stopped [ID_35199]

<!-- MR 10.4.0 - FR 10.3.11 -->

When a DataMiner Agent is deliberately stopped or stops working due to an error while a Cassandra Cluster migration is in progress, it will now be possible to resume that migration for certain storages instead of having to start it from scratch again.

For all types that are read in a partitioned way (currently alarms and trending), the migration progress will now be stored in *TokenRange.txt* files located in the `C:\Skyline DataMiner\Database` folder.

To resume a migration after restarting all DMAs in your DataMiner System, do the following:

1. Start *SLCCMigrator.exe* (which is located in the `C:\Skyline DataMiner\Tools\` folder).
1. Initialize all the DMAs in the list.
1. Click *Start Migration*.

> [!NOTE]
>
> - When a migration is resumed, the UI does not know how many rows were already migrated. Therefore, when a migration is resumed, it will erroneously display that 0 rows have been migrated so far.
> - When a DMA is initialized, a file named *SavedState.xml* will be created in the `C:\Skyline DataMiner\Database` folder. *SLCCMigrator.exe* will use this file to determine the point from which a migration has to be resumed.

### Fixes

#### Not all Protocol.Params.Param.Interprete.Others tags would not be read out [ID_36797]

<!-- MR 10.2.0 [CU20]/10.3.0 [CU8] - FR 10.3.11 -->

Not all [Protocol.Params.Param.Interprete.Others](xref:Protocol.Params.Param.Interprete.Others) tags would not be read out, which could lead to unexpected behavior.

#### SLElement could read and write to the same memory blocks on different threads [ID_37180]

<!-- MR 10.3.0 [CU8] - FR 10.3.11 -->

In some cases, SLElement could read and write to the same memory blocks on different threads, causing a serialized parameter update to get into a corrupt state.
