# HomeAssistant - SamsungTV Tizen Component

***app_list guide***
---------------

**Note:** Although this is an optional value, **it is highly recommended to set it manually**, even if in some (rare) cases the app list can be gotten from the TV successfully.

The `app_list` is used to set apps that you have installed on your TV. The app names can be associated with 2 types of IDs that Samsung TVs support: numerical IDs and alphanumerical IDs.

An application normally has both a numerical ID and an alphanumerical ID associated with it.

Here are some known lists of app IDs: [List 1](https://github.com/tavicu/homebridge-samsung-tizen/issues/26#issuecomment-447424879), [List 2](https://github.com/Ape/samsungctl/issues/75#issuecomment-404941201)

Here are 3 examples values for `app_list`:
- `'{"Netflix": "11101200001", "Prime Video": "3201512006785", "Spotify": "3201606009684"}'`
- `'{"Netflix": "org.tizen.netflix-app", "Prime Video": "org.tizen.ignition", "Spotify": "3201606009684"}'`
- `'{"Netflix": "11101200001/org.tizen.netflix-app", "Prime Video": "3201512006785/org.tizen.ignition", "Spotify": "3201606009684"}'`

(the last one is the prefered method, which includes both numerical and alphanumerical IDs, for increased support of this component)

In order to understand these example values, you must first understand what these IDs are used for.

An app ID is used to start the app on the TV and also to identify the running app on the TV.

To run the app on the TV, both numerical and alphanumerical IDs can be used, although there are some rare cases (for some select applications, such as "Prime Video") where the alphanumerical ID won't work to start the app, while the numerical ID will work.

To get the running app from the TV, two different ways are used:
- one works only with numerical IDs by doing HTTP polling on the TV (1 request for each app in `app_list`), this is a lengthy task that should be avoided if possible (this can be completely avoided by setting `scan_app_http` to `False` in your component's config)
- another works only with the alphanumerical IDs by getting the running app from the SmartThings API (requires SmartThings API enabled in your component's config)

There is only one rare case, for a few apps (like "Prime Video", the same case explained in how running the app works) where the numerical ID will work to start the app, but not to identify the running app, while it's alphanumerical ID will work to get the running app from the SmartThings API. It is for this case that we allow setting both numerical and alphanumerical IDs at the same time if you wish, which will handle this rare case correctly.
