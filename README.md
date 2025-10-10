# locatio-Alarm
notify where i reach 

Here’s the short, practical overview of how the app works and what each part does:

What it does
•  Search any Indian place: Uses Nominatim (OSM) to fetch suggestions and coordinates.
•  Show route: Uses OSRM to display driving distance (km) and time (min) from your current location.
•  Location alarms: Creates a geofence around the selected place; rings on arrival and shows an arrival notification.
•  Ongoing status: Foreground service notification shows active alarms and has “Delete All”.
•  Delete controls: Delete Alarm (per place) removes its geofence, storage entry, and selection (permanent).
•  Sound and settings: Pick custom sound (persisted URI), set radius, toggle vibration.

Key files
•  Screens: MainActivity (home), AlarmsActivity (list), SettingsActivity (radius/sound), AboutActivity (info)
•  Geofence + notifications: GeofenceBroadcastReceiver (arrival), LocationAlarmService (ongoing), NotificationActionReceiver (Delete All)
•  Networking: RetrofitClient, net/NominatimApi (+ NominatimResult), net/OsrmApi (+ OsrmResponse)
•  Storage: AlarmStorage (alarms), SettingsStore (selected place, radius, vibration, sound)

Main flows
•  Set alarm: MainActivity → geofence add → AlarmStorage add → update persistent notification
•  Arrival: GeofenceBroadcastReceiver → remove geofence → remove alarm → arrival notification
•  Proximity heads‑up: OSRM check every ~45s (only rings if selected name is still an active alarm)
•  Delete alarm: Button in Route card → remove geofence + alarm + clear selection → update UI + notification
•  Delete all: Notification button → removes all geofences + alarms + stops sound

Permissions
•  INTERNET, ACCESS_NETWORK_STATE
•  ACCESS_FINE_LOCATION (+ ACCESS_BACKGROUND_LOCATION for geofences)
•  POST_NOTIFICATIONS
•  FOREGROUND_SERVICE (+ LOCATION type)

Styling
•  Dark indigo→navy gradient background
•  Liquid-glass cards, chips, and bottom nav with active indicator
•  Custom gradient notification card

That’s it. Tell me what you want to tweak (e.g., per‑alarm radius, map preview, pause alarms) and I’ll give the exact steps.
