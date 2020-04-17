With retries, logger, bot check (manual intervention)
```
def get_soup(url: str):
    global logger, SESSION, RETRIES

    if RETRIES == 3:
        return None
    try:
        if not SESSION:
            SESSION = requests.Session()
            SESSION.headers.update(HEADERS)
        r = SESSION.get(url)
        if r.status_code >= 400:
            time_gap() # random sleep time
            manual_check()
            return get_soup(url)
        else:
            RETRIES = 0
            return BeautifulSoup(SESSION.get(url, timeout=30).text, 'lxml')
    except Exception as e:
        RETRIES = RETRIES + 1
        logger.error(e)
        return get_soup(url)

# sample check
def manual_check():
    global SESSION

    print()
    cookie = input('Paste cookie or ENTER: ')
    if cookie:
        SESSION.headers.update({'cookie': cookie})
    print()
```