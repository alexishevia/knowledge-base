# Uplynk Events Regex
Note: these regexes were converted to `Field extractions` for the `aws:s3` sourcetype. That allows us to do the extractions without adding a regex to every query.

Uplynk logs documentation:
  https://support.uplynk.com/doc_log_file_delivery.html#events

## slicing_began
```
index="uplynk" slicing_began | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>slicing_began)\t(?<job_type>[^\t]+)\t(?<asset_id>[^\t]+)\t(?<external_id>[^\t]+)\t(?<channel_id>[^\t]+)\t(?<description>[^\t]+)\t(?<slicer_software_id>[^\t]+)\t(?<slicer_version>[^\t]+)\t(?<event_id>[^\t]+)$"
```

## slicing_ended
```
index="uplynk" slicing_ended | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>slicing_ended)\t(?<asset_id>[^\t]+)\t(?<had_errors>[^\t]+)\t(?<slices>[^\t]+)$"
```

## asset_play_started
```
index="uplynk" asset_play_started | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>asset_play_started)\t(?<asset_id>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<channel_id>[^\t]+)\t(?<asset_is_ad>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)\t(?<playing_owner_id>[^\t]+)\t(?<event_id>[^\t]+)$"
```

## channel_play_started
```
index="uplynk" channel_play_started | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>channel_play_started)\t(?<channel_id>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)$"
```

## channel_ping
```
index="uplynk" channel_ping | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>channel_ping)\t(?<channel_id>[^\t]+)\t(?<asset_id>[^\t]+)\t(?<bucket_number>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)$"
```

## event_play_started
```
index="uplynk" event_play_started | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>event_play_started)\t(?<event_id>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)$"
```

## event_ping
```
index="uplynk" event_ping | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>event_ping)\t(?<event_id>[^\t]+)\t(?<asset_id>[^\t]+)\t(?<bucket_number>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)$"
```

## slice_played
```
index="uplynk" slice_played | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>slice_played)\t(?<asset_id>[^\t]+)\t(?<slice_number>[^\t]+)\t(?<is_live>[^\t]+)\t(?<user_ip>[^\t]+)\t(?<player_user_agent>[^\t]+)\t(?<player_referrer_url>[^\t]+)\t(?<euid>[^\t]+)\t(?<session_id>[^\t]+)\t(?<playing_owner_id>[^\t]+)\t(?<channel_id>[^\t]+)\t(?<event_id>[^\t]+)$"
```

## session_created
```
index="uplynk" session_created | rex field=_raw "^(?<date>[^\t]+)\t(?<time>[^\t]+)\t(?<event_name>session_created)\t(?<session_id>[^\t]+)\t(?<content_id>[^\t]+)\t(?<content_type>[^\t]+)\t(?<playing_owner_id>[^\t]+)\t(?<user_agent>[^\t]+)\t(?<euid>[^\t]+)\t(?<referer>[^\t]+)\t(?<user_ip>[^\t]+)$"
```
