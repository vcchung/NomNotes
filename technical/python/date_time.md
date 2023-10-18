# Date Time

- convert timezone and print date time
```
def convert_utc_to_hkt(input: str) -> str:
    hk_tz = timezone("Asia/Hong_Kong")
    utc_time = timezone("UTC").localize(datetime.strptime(input, "%Y-%m-%dT%H:%M:%S.%f"))
    return utc_time.astimezone(hk_tz).strftime('%Y-%m-%d %H:%M:%S %Z')
```
