# GCP_SDK_Instance_Disk_Snapshot_Management


## Google Cloud Platform SDK: Instance, Disk, and Snapshot Management

This repository demonstrates how to manage **instances**, **disks**, and **snapshots** using **Google Cloud SDK**. It covers API calls, input/output types, execution behaviors, and whether the operations are synchronous or asynchronous.

### Table of Contents
1. [Creating Credentials from Service Account Info](#1-creating-credentials-from-service-account-info)
2. [Retrieving Instance Information](#2-retrieving-instance-information)
3. [Retrieving Disk Details](#3-retrieving-disk-details)
4. [Creating a Snapshot](#4-creating-a-snapshot)
5. [Initiating Snapshot Creation](#5-initiating-snapshot-creation)
6. [Checking Operation Result](#6-checking-operation-result)
7. [Retrieving Snapshot Information](#7-retrieving-snapshot-information)

### References
- [Google Cloud Compute v1 SDK Documentation for Snapshots](https://cloud.google.com/python/docs/reference/compute/latest/google.cloud.compute_v1.types.Snapshot)
- [Google Cloud Compute REST API for Snapshot Insert](https://cloud.google.com/compute/docs/reference/rest/beta/snapshots/insert)

---

#### 1. Creating Credentials from Service Account Info

This section explains how to create Google Cloud service account credentials from a JSON object containing service account information.

```python
from google.oauth2 import service_account

storage_credentials = service_account.Credentials.from_service_account_info(info)
```

**Input:**  
- `info`: A dictionary containing the service account key information (usually parsed from a JSON file).

**Return Type:**  
- `Credentials`: An object used for authenticating requests to Google Cloud.

**Execution:**  
- Synchronous.

---

#### 2. Retrieving Instance Information

Use the following API call to get information about a specific instance.

```python
instance_info = instances_client.get(project='my-project', zone='us-central1-a', instance='my-instance')
```

**Input:**  
- `project`: Google Cloud project ID (string).  
- `zone`: Zone of the instance (string).  
- `instance`: Instance name (string).

**Return Type:**  
- `Instance`: An object representing the details of the requested instance.

**Execution:**  
- Synchronous.

---

#### 3. Retrieving Disk Details

Retrieve detailed information about a specific disk.

```python
disk_details = disks_client.get(project='my-project', zone='us-central1-a', disk='my-disk')
```

**Input:**  
- `project`: Google Cloud project ID (string).  
- `zone`: Zone of the disk (string).  
- `disk`: Disk name (string).

**Return Type:**  
- `Disk`: An object representing the details of the requested disk.

**Execution:**  
- Synchronous.

---

#### 4. Creating a Snapshot

Create a snapshot of a specific disk using the following code.

```python
snapshot = compute_v1.Snapshot(
    name='my-snapshot',
    source_disk='projects/my-project/zones/us-central1-a/disks/my-disk',
    labels={'env': 'prod'},
    description='Snapshot of production disk',
    storage_locations=['us-central1']
)
```

**Input:**  
- `name`: Name of the snapshot (string).  
- `source_disk`: The source disk to snapshot (string).  
- `labels`: Key-value pairs (dict).  
- `description`: Snapshot description (string).  
- `storage_locations`: Locations to store the snapshot (list).

**Return Type:**  
- `Snapshot`: An object representing the newly created snapshot.

**Execution:**  
- Synchronous.

---

#### 5. Initiating Snapshot Creation

Use this call to initiate the snapshot creation.

```python
operation = snapshots_client.insert(project='my-project', snapshot_resource=snapshot)
```

**Input:**  
- `project`: Google Cloud project ID (string).  
- `snapshot_resource`: Snapshot object.

**Return Type:**  
- `Operation`: An object that represents the ongoing snapshot creation process.

**Execution:**  
- Asynchronous.

---

#### 6. Checking Operation Result

To wait for the completion of a snapshot creation, use the following code.

```python
operation.result()
```

**Return Type:**  
- `Snapshot`: The completed snapshot object.

**Execution:**  
- Blocking (waits until the operation is complete).

---

#### 7. Retrieving Snapshot Information

Retrieve details of a specific snapshot using this call.

```python
snapshot_info = snapshots_client.get(project='my-project', snapshot='my-snapshot')
```

**Input:**  
- `project`: Google Cloud project ID (string).  
- `snapshot`: Name of the snapshot (string).

**Return Type:**  
- `Snapshot`: An object containing the details of the snapshot.

**Execution:**  
- Synchronous.

---

