# Set proxy

## powershell - command alias

```powershell
PS> notepad $profile
```

```powershell
function setproxy {
    $env:http_proxy = "http://127.0.0.1:7890"
    $env:https_proxy = "http://127.0.0.1:7890"
    [System.Net.WebRequest]::DefaultWebProxy = New-Object System.Net.WebProxy("http://127.0.0.1:7890")
}

function disproxy {
    $env:http_proxy = $null
    $env:https_proxy = $null
    [System.Net.WebRequest]::DefaultWebProxy = $null
}

function ghgt {
    setproxy
    git push origin main
    git push gitee main
    disproxy
}
```

```
setproxy -> 设置代理
disproxy -> 取消代理
ghgt -> 推送到 github & gitee
```
