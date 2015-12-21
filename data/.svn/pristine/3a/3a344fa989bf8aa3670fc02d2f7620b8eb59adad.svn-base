/**
 * 获取应用程序data目录
 **/
function getDataDir()
{
    if(!isValue(typeof Qt))
        return "";

    return Qt.getDataDir();
}

/**
 * 获取验证码目录
 **/
function getCodeDir()
{
    if(!isValue(typeof Qt))
        return "";

    return Qt.getCodeDir();
}

/**
 * 获取小号
 **/
function getAccount()
{
    if(!isValue(typeof Qt))
        return "";

    return toJson(Qt.getAccount());
}

/**
 * 获取用户信息
 **/
function getUser()
{
    if(!isValue(typeof Qt))
        return "";

    return toJson(Qt.getUser());
}

/**
 * 获取本地文件内容
 * @param fileName 文件名
 * @return 如果Qt存在返回文件内容
 **/
function getFile(fileName)
{
    if(!isValue(typeof Qt))
        return "";

    return Qt.getFile(fileName);
}

/**
 * 获取LANGUAGE文件名
 **/
function getFileLan()
{
    if(!isValue(typeof Qt))
        return "";

    return Qt.getFileLan();
}

function setFileLan(value)
{
    if(!isValue(typeof Qt))
        return "";

    Qt.setFileLan(value);
}

/**
 * 保存文件内容
 **/
function saveFile(fileName,content)
{
    if(!isValue(typeof Qt))
        return "";

    return Qt.saveFile(fileName,content);
}

/**
 * 获取验证码保存路径
 **/
function getCodeFile()
{
    if(!isValue(typeof Qt))
        return "";

    return toJson(Qt.getCodeList());
}

/**
 * 输出日志到console
 * @param msg 输出内容
 **/
function log(msg)
{
    if(isValue(typeof Qt))
        Qt.slLog(msg);
}

/**
 * 获取服务器地址
 **/
function getServerUrl()
{
    mServerUrl = isValue(typeof Qt) ? Qt.getServerUrl() : mServerUrl;
}

/**
 * 获取用户名
 **/
function getUsername()
{
    if(!isValue(typeof Qt))
        return;

    return Qt.getUsername();
}

/**
 * 首页调用
 **/
function getTipUsername()
{
    var username = getUsername();

    if (!username) {
        return;
    }

    if(username.length == 32)
    {
        username = $.t("main.anonymous");
        mbox($.t("main.newbie"),3);
    }

    $("#title_username").html(username);

    return username;
}

/**
 * 获取密码加密方式
 * @param password 密码
 * @param code 验证码
 **/
function getPasswordEncode(password,code)
{
    if(!isValue(typeof Qt))
        return;

    return Qt.getPasswordEncode(password,code);
}

/**
 * 获取远程数据
 * @param callbackFunc 回调函数，字符串
 * @param url 远程地址
 * @param post post数据
 **/
function getUrl(callbackFunc,url,post)
{
    if(!isValue(typeof Qt))
        return;

    post = isValue(typeof post) ? post : "";
    Qt.getUrl(callbackFunc, url, post);
}

function setUserInfo(key,value)
{
    if (!Qt) return;

    var userInfo = getUser();
    userInfo[key] = value;

    Qt.setUserInfo(JSON.stringify(userInfo));
}

/**
 * 获取用户是否使用自动码
 **/
function getUseCode()
{
    if (!Qt) {
        return false;
    }

    var userInfo = getUser();
    return userInfo.use_code > 0;
}

/**
 * 设置用户使用自动码
 * @param open
 **/
function setUseCode(open)
{
    setUserInfo('use_code',open);
    jsonp('user/use_code.php?id=' + open);
}

/**
 * 查询是否自动开启
 **/
function getOpen()
{
    if(!isValue(typeof Qt))
        return;

    return Qt.getOpen();
}

/**
 * 设置开机启动
 * @param open 不为空就是开机
 **/
function setOpen(open)
{
    if(!isValue(typeof Qt))
        return;

    return Qt.setOpen(open);
}

/**
 * 设置登录帐号和密码
 * @param username 帐号
 * @param password 密码
 **/
function setUser(username,password)
{
    if(!isValue(typeof Qt))
        return;

    Qt.setUser(username,password);
    getUsername();
}
