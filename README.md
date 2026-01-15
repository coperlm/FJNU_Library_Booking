# FJNU_Library_Booking
超星图书馆座位预约脚本

## 注意

1. 这份代码只支持滑块验证码，但是手动预约需要点按式验证码，又但是这份代码确实能用（估计是旧的验证码没被完全ban掉）
2. 只支持座位，而非静音仓
3. 代码来源：https://github.com/bear-zd/ChaoXingReserveSeat
4. 2026/1/14亲测能用

## 如何使用

### 本地部署方式

去看[原作者](https://github.com/bear-zd/ChaoXingReserveSeat/blob/rebuild/README.md)的吧~

### github actions部署方式

1.**fork该仓库**

2.**修改config.json**：这个仿照之前的方式进行修改即可，但是注意，username和password请留空或者随便填以防止泄漏个人账号密码。（具体的需要填写在自己repo的settings中）。时间什么也是需要修改（修改到仓库中）不要忘记。

3.**配置账号密码**：在settings->secrets and variables->Repository secrets 创建两个secret keys。名称分别为USERNAMES，PASSWORDS，填写自己的账号和密码即可。（如果有多个用户，请使用,(英文逗号)隔开，如果密码中有逗号可能会出现问题）。

```
xxxxxxx,xxxxxxx
```

4.**运行action**：在action -> auto_reserve -> run workflows 选择main分支即可。


## config配置
之后编辑config.json并填写座位预约相关信息即可
```json
{
    "reserve": [
        {"username": "XXXXXXXX", //https://passport2.chaoxing.com/mlogin?loginType=1&newversion=true&fid=&  在这个网站查看是否可以顺利登陆 
        "password": "XXXXXXXX",
        "time": ["08:00","22:00"], // 预约的起始时间
        "roomid":"2609", //2609:四楼外圈,5483:四楼内圈,2610:五楼外圈,5484:五楼内圈
        "seatid":"002", // 注意要用0补全至3位数，例如6号座位应该填006
        "daysofweek": ["Monday" , "Tuesday", "Wednesday", "Thursday", "Friday"]
        },
        {"username": "xxxxxxxxxx",
        "password": "xxxxxxxxx",
        "time": ["20:00","21:00"],
        "roomid":"5483",
        "seatid":["056"],
        "daysofweek": ["Saturday" , "Sunday"]
    }
}
```
参考前面的运行方式即可。


## 高级设置

在main.py中有四个参数可以选择

```python
SLEEPTIME = 0.2 # 每次抢座的间隔
ENDTIME = "07:01:00" # 根据学校的开始预约座位时间+1min即可

ENABLE_SLIDER = False # 是否有滑块验证，设置为True开启滑块验证
MAX_ATTEMPT = 4 # 最大尝试次数
```
可以直接进行修改，但是不建议把**SLEEPTIME**设置太小。
