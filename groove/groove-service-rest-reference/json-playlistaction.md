---
title: PlaylistAction JSON object | Groove Services
description:  Learn about PlaylistActiob JSON object in Groove Music API.
keywords: groove music, groove api, groove playlistaction json
author: sakley
ms.assetid: 700c43a1-e5d7-4bed-b65c-ed5745370379
---

# PlaylistAction (JSON)     
The input element for every playlist action request: create, update, and delete.  
A PlaylistAction contains playlist metadata and a list of actions to perform on the tracks in the playlist.

## PlaylistAction
The PlaylistAction object has the following specification.

| **Member**           | **Type**                                                             | **Description**                                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Id                   | string                                                               | Required. ID of the playlist (required for update and delete).                                                                                                                         |
| CollectionStateToken | string                                                               | *Optional*. Token indicating the current version of the collection.                                                                                                                      |
| Name                 | string                                                               | *Optional*. Name of the playlist.                                                                                                                                                        |
| IsPublished          | Boolean value                                                        | *Optional.* Whether the playlist is public or not.                                                                                                                                       |
| InsertBeforeTrackId  | string                                                               | *Optional* When reordering tracks, track before which you want to insert the tracks specified in the TrackActions field. Can be null if you want to insert at the end of the playlist. |
| TrackActions         | List of [TrackAction](JSON-TrackAction.md) | Optional. List of actions to perform on the playlist's tracks.                                                                                                                         |

## Sample JSON syntax
```json
{
  "Id": "music.playlist.56c99764-800a-00fe-552f-ee11db9370d1",
  "TrackActions": [
    {
      "Id": "music.AQQfj2DtARB5ZkGFCMHea2k8Xge5PqgAAQ",
      "Action": "Delete"
    },
    {
      "Id": "music.2DEBEA07-0100-11DB-89CA-0019B92A3933",
      "Action": "Add"
    }
  ]
}
```

#### Parent
[Groove Service REST Reference](overview.md)

#### Reference
[/1/content/{namespace}/collection/playlists/create](uri-create-playlist.md)  
[/1/content/{namespace}/collection/playlists/delete](uri-delete-playlist.md)  
[/1/content/{namespace}/collection/playlists/update](uri-update-playlist.md)
