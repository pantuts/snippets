```
from pythonjsonlogger import jsonlogger
import daiquiri
import daiquiri.formatter
import logging

LOG_DIR = './logs'
LOG_FILENAME = 'logs'
LOG_FILENAME_EXT = 'json'
LOG_MAX_SIZE_BYTES = 1.5e+7  # 15mb
LOG_BACKUP_COUNT = 10
logfile = os.path.join(LOG_DIR, '{}_{}.{}'.format(LOG_FILENAME, now, LOG_FILENAME_EXT))


def setup_logger(name: str, level=logging.DEBUG):
    daiquiri.setup(level=level, outputs=(
        daiquiri.output.Stream(sys.stdout),
        daiquiri.output.RotatingFile(logfile, formatter=jsonlogger.JsonFormatter(
            fmt=LOG_FORMAT),
            level=level, max_size_bytes=LOG_MAX_SIZE_BYTES, backup_count=LOG_BACKUP_COUNT
        )
    ))
    logger = daiquiri.getLogger(name)
    return logger
```