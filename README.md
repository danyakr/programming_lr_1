# Реализация удаленного импорта собственного пакета

1. activation_script
```
import sys
import requests
import importlib.util

class URLLoader:
    def __init__(self, url):
        self.url = url

    def get_code(self):
        response = requests.get(self.url)
        response.raise_for_status()
        return response.text

def url_hook(path):
    if path.startswith("http://"):
        return URLLoader(path)
    return None

# url_hook в sys.path_hooks
sys.path_hooks.append(url_hook)
sys.path.append("http://localhost:8000")
```

2. myremotemodule

```
def myfoo():
    author = "krasnikovdanya"
    print(f"{author}'s module is imported")
```

![image](https://github.com/user-attachments/assets/75f89f86-8316-4c62-9bb5-af26d5b1bfa9)

![image](https://github.com/user-attachments/assets/c362b04d-ef28-4d08-a7be-3e9d85e45018)

![image](https://github.com/user-attachments/assets/41417026-85c5-44a9-bb90-8f8266a99ee4)

![image](https://github.com/user-attachments/assets/d622d7be-b3e8-416d-b98b-1e96e41a181c)



