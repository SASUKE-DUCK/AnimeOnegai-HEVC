# AnimeOnegai-HEVC
```bash
from curl_cffi import requests as s_requests

# Change the User-Agent to mimic a request from an Android application
headers = {
    'User-Agent': 'Mozilla/5.0 (Linux; Android 10; Mobile; rv:81.0) Gecko/81.0 Firefox/81.0',
    'Host': 'api.animeonegai.com',
    'Origin': 'https://www.animeonegai.com',
    'Referer': 'https://www.animeonegai.com/',
    'Accept': 'application/json',
    'Content-Type': 'application/json',
}

# Assume you have the 'episode' variable defined previously
episode_id = episode["video_entry"]
api_url = f'https://api.animeonegai.com/v1/media/{episode_id}'

params = {
    'param1': 'value1',
    'param2': 'value2',
}

# Perform the GET request
response_subtitle = s_requests.get(api_url, headers=headers, params=params)

# Check if the request was successful (status code 200)
if response_subtitle.status_code == 200:
    # Parse the JSON response
    json_subtitle = response_subtitle.json()
    dash_url = json_subtitle.get("dash", "")

    # Define suffixes for different formats
    suffix_hevc = "_hevc.mpd"
    suffix_m3u8 = "_hevc.m3u8"
    suffix_hdr = "_hdr.mpd"
    suffix_sdr = "_sdr.mpd"
    suffix_dv = "_dv.mpd"
    suffix_hlg = "_hlg.mpd"

    # Perform requests for different formats
    response_hevc = s_requests.get(dash_url + suffix_hevc, headers=headers)
    dash_m3u8_url = dash_url.replace(suffix_hevc, suffix_m3u8)
    dash_hdr_url = dash_url.replace(suffix_hevc, suffix_hdr)
    dash_sdr_url = dash_url.replace(suffix_hevc, suffix_sdr)
    dash_dv_url = dash_url.replace(suffix_hevc, suffix_dv)
    dash_hlg_url = dash_url.replace(suffix_hevc, suffix_hlg)

    # You can use the variables dash_m3u8_url, dash_hdr_url, dash_sdr_url, dash_dv_url, dash_hlg_url as needed.
else:
    print(f"Error while making the request: {response_subtitle.status_code}")```
