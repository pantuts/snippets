# Libraries to study
* https://github.com/pytoolz/toolz
* https://github.com/samuelcolvin/pydantic
* https://fastapi.tiangolo.com/
* https://airshare.readthedocs.io/en/latest/

# beautifulsoup
[bs4.md](bs4.md)

# base64
```
def b64_file(full_path: str):
    try:
        with open(full_path, 'rb') as f:
            b = base64.b64encode(f.read())
        return b
    except Exception as e:
        return None
```

# csv/json
CSV to JSON
```
def csv_to_json(full_path: str):
    data = []
    with open(full_path, 'r') as c:
        reader = csv.DictReader(c)
        for r in reader:
            data.append(json.loads(json.dumps(r)))
    return data
```
JSON to CSV
```
def dump_data_to_csv(data: Union[List, Dict], full_path: str):
    try:
        exists = os.path.isfile(full_path)
        with open(full_path, 'a+') as f:
            writer = csv.DictWriter(f, fieldnames=CSV_HEADERS)
            if not exists:
                writer.writeheader()
            if isinstance(data, dict):
                writer.writerow(data)
            elif isinstance(data, list):
                for o in data:
                    writer.writerow(o)
        return True
    except Exception as e:
        return False
```

# daiquiri
[daiquiri.md](daiquiri.md)

# json
Dump data to json file
```
def dump_data_to_json(obj: Dict, full_path: str):
    with open(full_path, 'w') as f:
        json.dump(obj, f)
```

# mailjet
[mailjet.md](mailjet.md)

# os
List folders
```
next(os.walk('FOLDER'))[1]
```
Create directory
```
def create_dir(d: str):
    if not os.path.exists(d):
        os.mkdir(d)
```

# selenium
```
from selenium import webdriver
from selenium.common.exceptions import NoSuchElementException, TimeoutException
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.common.proxy import Proxy, ProxyType
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import WebDriverWait

def set_driver(headless=True, proxy=None, cache_dir=None):
    options = Options()
    if headless:
        options.add_argument('--headless')
    options.add_argument('--disable-dev-shm-usage')
    options.add_argument('--no-sandbox')
    if proxy:
        options.add_argument(f'--proxy-server={proxy.get("type")}://{proxy.get("ip")}:{proxy.get("port")}')
    if cache_dir:
        options.add_argument(f'--disk-cache-dir=cache_dir')
    options.add_argument(f'user-agent="Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36"')
    # disable images
    prefs = {}
    prefs["profile.default_content_settings"] = {"images": 2}
    prefs["profile.managed_default_content_settings"] = {"images": 2}
    prefs['disk-cache-size'] = 52428800
    options.experimental_options["prefs"] = prefs

    if platform.system() == 'Windows':
        driver = webdriver.Chrome(executable_path='./chromedriver.exe', options=options)
    else:
        driver = webdriver.Chrome(options=options)
    return driver
```
Wait
```
WebDriverWait(driver, 15).until(EC.presence_of_element_located((By.XPATH, xpath)))
```

# shutil
Zip folder
```
def zip_folder(d: str, fname: str):
    if os.path.exists(d):
        try:
            make_archive(f'/tmp/{fname}', 'zip', d)
            return True
        except Exception as e:
            return False
    return False
```

# sleep
```
def time_gap():
    for remaining in range(random.randint(1, 7), 0, -1):
        sys.stdout.write("\r")
        sys.stdout.write('Resuming in {:2d}\t'.format(remaining))
        sys.stdout.flush()
        time.sleep(1)
```

# tqdm
Specifically for image and video. Can be used on other, edit accordingly.
```
def download(_type, ref, url, folder):
    fname = unquote(url).split('/')[-1].split('?')[0]
    fname = os.path.join(folder, fname)
    if _type == 'image':
        headers = {
            'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36'
        }
    elif _type == 'video':
        headers = {
            'Accept': '*/*',
            'Accept-Encoding': 'identity;q=1, *;q=0',
            'Accept-Language': 'en-US,en;q=0.9',
            'Connection': 'keep-alive',
            'dnt': '1',
            'Host': list(filter(None, url.split('/')))[1],
            'Referer': ref,
            'Sec-Fetch-Dest': 'video',
            'Sec-Fetch-Mode': 'no-cors',
            'Sec-Fetch-Site': 'cross-site',
            'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36'
        }
    session = requests.Session()
    resp = session.get(url, headers=headers, stream=True)

    try:
        with tqdm.wrapattr(open(fname, 'wb'), 'write',
                    miniters=1, desc=os.path.basename(fname),
                    total=int(resp.headers.get('content-length', 0))) as fout:
            for chunk in resp.iter_content(chunk_size=1024):
                fout.write(chunk)
    except Exception as e:
        print(e)
        try:
            os.remove(fname)
        except Exception:
            pass
```
