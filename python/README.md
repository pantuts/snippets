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
