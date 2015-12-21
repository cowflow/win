/**全局页面传参**/
var mParam={};
/** 服务器地址 **/
var mServerUrl = "http://client.cowflow.com/";

/** 当前data目录 **/
var mDataDir = "";

/** 当前语言版本 **/
var mLan = "zh";

/** 验证码名 **/
var mCodeName = "";
var mCodeValue = "";

/** 保存CHECKBOX的已选的所有ID **/
var mIDBox = "";

/** 最后选择的ID **/
var mID = "";

/** 当前页面 **/
var nowPage = "";

/**
 * 禁止右键菜单
 **/
function nocontextmenu()
{
    event.cancelBubble = true
    event.returnValue = false;

    return false;
}

/**
 * 禁止右键菜单
 **/
function norightclick(e)
{
    if (window.Event)
    {
        if (e.which == 2 || e.which == 3)
            return false;
    }
    else
    if (event.button == 2 || event.button == 3)
    {
        event.cancelBubble = true
        event.returnValue = false;
        return false;
    }
}

/**
 * 禁止右键菜单
 **/
function norightmenu()
{
    if (window.Event)
        document.captureEvents(Event.MOUSEUP);

    document.oncontextmenu = nocontextmenu;  // for IE5+
    document.onmousedown = norightclick;  // for all others
}

function pageInit(css)
{
    css = css ? css : ".page-content";
    $('#main').i18n();
    $('button').tooltip();

    $('form').submit(function(event){
        return false;
    });

 //   formEnter(css,buttonSubmit);
}

/**
 * 模块对话框
 * @param path  本地HTML文件名
 **/
function pbox(fileName)
{
    var div_id = 'mbox_page';
    var data = '<br><div id="'+div_id+'">loading..</div><script>$("#mbox_page").load(\''+fileName+'.html?_t='+microTime()+'\',\'\',function(){pageInit(\'#mbox_page\');});</script>';

    bootbox.dialog({
        message: data
    });
}

/**
 * 隐藏所有bootbox
 **/
function hidePbox()
{
    bootbox.hideAll();
}

/**
 * 获取外部传参
 * @param name
 **/
function getQuery(name)
{
    // 如果链接没有参数，或者链接中不存在我们要获取的参数，直接返回空
    if(location.href.indexOf("?")==-1 || location.href.indexOf(name+'=')==-1)
        return '';

    // 获取链接中参数部分
    var queryString = location.href.substring(location.href.indexOf("?")+1);

    // 分离参数对 ?key=value&key2=value2
    var parameters = queryString.split("&");

    var pos, paraName, paraValue;
    for(var i=0; i<parameters.length; i++)
    {
        // 获取等号位置
        pos = parameters[i].indexOf('=');
        if(pos == -1) { continue; }

        // 获取name 和 value
        paraName = parameters[i].substring(0, pos);
        paraValue = parameters[i].substring(pos + 1);

        // 如果查询的name等于当前name，就返回当前值，同时，将链接中的+号还原成空格
        if(paraName == name)
            return unescape(paraValue.replace("/+/g", " "));
    }
    return '';
}

/**
 * 毫秒时间
 **/
function microTime()
{
    return Math.round(new Date().getTime());
}

/**
 * 秒时间
 **/
function secTime()
{
    return Math.round(microTime() / 1000);
}

/**
 * 判定值是否存在
 * @param value 判断值 判断的值必须是 typeof value
 **/
function isValue(value)
{
    return value != "undefined";
}

/**
 * 获取当前语言版本
 **/
function getLan()
{
    mLan = getFileLan();
    mLan = mLan == "" ? "zh" : mLan;
    return mLan;
}

/**
 * 显示Code Bell的跳动
 **/
function showCodeBell()
{
    $('#code_bell').addClass('icon-animated-bell');
    $('#code_badge').show();
}

/**
 * 隐藏Code Bell的跳动
 **/
function hideCodeBell()
{
    $('#code_bell').removeClass('icon-animated-bell');
    $('#code_badge').hide();
}

/**
 * 设置当前语言版本
 * @param value 语言
 **/
function setLan(value)
{
    mLan = value;
    setFileLan(value);
}

/**
 * 开始异步提交的循环动画
 **/
function startLoading()
{
    $("button").each(function(){
        if($(this).prop("class").indexOf('close') == -1) {
            $(".loading-key").hide();
            $(this).isLoading();
        }
    });

}

/**
 * 停止异步提交的循环动画
 **/
function endLoading()
{
    $("button").each(function(){
        $(this).isLoading( "hide" );
    });

    $(".isloading-wrapper").each(function(){
        $(this).hide();
    });
}

/**
 * 获取远程JSON通过模板填充指定目标
 * @param url 远程地址
 * @param template 模板编号
 * @param target 目标编号
 * @param callback 回调
 **/
function jsonm(url,template,target,callback)
{
    jsonp(url,function (json) {
        var html = "";
        try {
            if (json.data.length == 0) {
                json.empty = true;
            }

            data = $(template).val();
            html = Mustache.to_html(data, json).replace(/^\s*/mg, '');
            $(target).html(html);

            var templatePage = template+"Page";
            var targetPage = target+"Page";
            if ($(templatePage).val() != "" && $(targetPage).prop('id')) {
                data = $(templatePage).val();
                html = Mustache.to_html(data, json).replace(/^\s*/mg, '');
                $(targetPage).html(html);
            }
        } catch (_error) {
            e = _error;
            html = e.toString();
            // mbox(html);
            mbox($.t("message.templateError"));
        }

        $('input.par').click(function(){
            var checked = $(this).prop('checked');
            $('input.sub').prop('checked', checked);
            setCheckBoxId();
        });

        $('input.sub').click(function(){
            setCheckBoxId();
        });

        $('#main').i18n();
        $('a').tooltip();

        if (callback) {
            callback(json);
        }
    });
}

function setCheckBoxId()
{
    mIDBox = "";
    $('input.sub').each(function(){
        if ($(this).prop('checked')) {
            mIDBox += $(this).prop('value') + ",";
            mID = $(this).prop('value');
        }
    });
}

function checkMID()
{
    mID = "";
    setCheckBoxId();

    if (mID == "") {
        mbox($.t("operation.pleaseSelectRow"));
        return false;
    }

    return true;
}

/**
 * 传递TEXT参数ENCODE
 **/
function paramEncode(data)
{
    return encodeURIComponent(Base64.encode(data));
}

/**
 * jsonp调用远程数据
 * @param url 网络地址
 * @param callback 回调函数 funciton(data)
 **/
function jsonp(url,callback)
{
    getServerUrl();

    url = url.indexOf("http") == 0 ? url : mServerUrl + url;
    url = url.indexOf("?") != -1 ? url + "&" : url + "?";
    url = url + "_l=" + getLan();

    log("UUrl:" + url);

    endLoading();
    startLoading();

    $.ajax({
        url:url,
        dataType:"jsonp",
        jsonp:"callback",
        timeout:15000,
        success:function(data)
        {
            endLoading();
            if (callback) {
                callback(data);
            }
        },
        error:function(jqXHR, exception)
        {
            msg = "";
            if (jqXHR.status === 0)
                msg ='Not connect.\n Verify Network.';
            else if (jqXHR.status == 404)
                msg = 'Requested page not found. [404]';
            else if (jqXHR.status == 500)
                msg = 'Internal Server Error [500].';
            else if (exception === 'parsererror')
                msg = 'Requested JSON parse failed.';
            else if (exception === 'timeout')
                msg = 'Time out error.';
            else if (exception === 'abort')
                msg = 'Ajax request aborted.';
            else
                msg ='Uncaught Error.\n' + jqXHR.responseText;

            if(msg != "")
                mbox($.t("message.networkError"));

            endLoading();
        }
    });
}

/**
 * 延迟调用指定函数
 * @param func 需要调用的函数
 * @param second 延迟的时间
 **/
function one(func,second)
{
    setTimeout(function()
    {
        func();
    },second * 1000);
}

/**
 * 判断是否为函数
 * @param fn 判断的值必须是isFunction(typeof fn)
 **/
function isFunction(fn)
{
    return fn == 'function';
}

/**
 * json字符串转成javascript数组
 * @param value
 **/
function toJson(value)
{
    return eval("(" + value + ")");
}

/**
 * 移出hightcharts的值
 **/
function removeHightcharts()
{
    $("svg > text").each(function(){
        if($(this).text() == "Highcharts.com")
        {
            $(this).text("");
        }
    });

    $(".highcharts-button").each(function(){
        $(this).hide();
            //console.log($(this));
    });
}

/** 加载次数，用于loadHtml的记录 **/
var loadTimes = 0;

/**
 * 加载本地页面，用于_main.html
@startuml
:隐藏tooltip-arrow;
:隐藏tooltip-inner;
:隐藏mainMneu所有菜单的激活;
:激活点击的菜单;

if (child != '') then 是
    :激活点击的子菜单;
endif

:加载指定的页面，加载完毕，加载语言包;
:loadTimes++;

if (Qt变量存在) then 是
    :Qt释放内存;
endif

if (loadTimes加载次数超过一百次) then 是
    :重新刷新整个页面;
endif
@enduml
 * @param parent 主菜单显示激活
 * @param child 子菜单显示激活
 **/
function loadHtml(parent,child,tag)
{
    child = !child ? "" : child;
    tag = !tag ? "" : "#" + tag;

    var page = child == "" ? parent : child;

    nowPage = "";//初始当前PAGE的翻页值

    $(".tooltip-arrow").hide();
    $(".tooltip-inner").hide();

    $('#mainMenu li').each(function(){
        $(this).attr('class','');
    });

    $('#main_' + parent).attr('class','active');
    if(child != "")
        $('#child_' + child).attr('class','active');

    $('.main-content').load(page + '.html'+tag+'?_t=' + microTime(),"",function(){
        pageInit();
    });

    loadTimes++;

    if(isValue(typeof Qt))
        Qt.clearMemory();

    if(loadTimes > 100)
        reloadMain();
}

/**
 * 重新加载页面
 **/
function reloadMain()
{
    location.reload(true);
}

/** 检查鼠标移动的时间 **/
var checkTouchTime = secTime() + 10;

/**
 * 当鼠标移动到画面，才执行指定的函数
 用于用户界面，不用频繁的调用远程接口。
 * @param func 指定运行的函数
 * @param intevalTime 间隔的时间
 **/
function touch(func,intevalTime)
{
    if(typeof intevalTime == 'undefined')
        intevalTime = 10;

    intevalTime = intevalTime < 3 ? 3 : intevalTime;

    $( ".page-content" ).mousemove(function(){
        if(secTime() < checkTouchTime)
            return;

        checkTouchTime = secTime() + intevalTime;
        func();
    });
}

function tbox(text)
{
    data = $.t(text);
    mbox(data);
}

/**
 * 确认框
 * @param text
 * @param fun
 **/
function mconfirm(text,fun)
{
    bootbox.confirm(text,function(result) {
        if(result) {
            fun();
        }
    });
}

/**
 * 右上角信息提示
 * @param text 信息内容
 * @param sec 持续时间
 **/
function mbox(text,sec)
{
    text = !text ? "" : text;
    sec = !sec ? 5 : sec;

    $.gritter.add({
        title: $.t("message.tip"),
        text: text,
        time: sec * 1000,
        class_name: 'gritter-info'
    });
}

/**
 * 加载菜单，用于_main.html
 * @param mainMenu 主菜单数组
 * @param childMenu 子菜单数组
 **/
function loadMenu(mainMenu,childMenu)
{
    var menuString = "";

    for(var i in mainMenu)
    {
        menuString +=
        '<li id="main_' + mainMenu[i].id + '" class="' + ( mainMenu[i].id == 'index' ? "active" : '' ) + '">' +
            '<a href="' + ( mainMenu[i].children ? "#" : 'javascript:loadHtml(\'' + mainMenu[i].id + '\',\'' + mainMenu[i].id + '\');' ) + '" ' + ( mainMenu[i].children ? ' class="dropdown-toggle"' : '' ) + '>' +
            '<i class="' + mainMenu[i].icon + '"></i>' +
            '<span class="menu-text"> ' + mainMenu[i].name + ' </span>' +
            '' + ( mainMenu[i].children ? '<b class="arrow fa fa-angle-down"></b>' : '' ) + '</a><b class="arrow"></b>';

        if( mainMenu[i].children )
        {
            menuString += '<ul class="submenu">';

            for(var j in childMenu)
            {
                if(childMenu[j].id == mainMenu[i].id)
                {
                    menuString +=
                    '<li id="child_' + childMenu[j].method + '" class="">' +
                        '<a href="javascript:loadHtml(\'' + mainMenu[i].id + '\',\'' + childMenu[j].method + '\');">' +
                        '<i class="menu-icon fa fa-caret-right"></i>' +
                        ' ' + childMenu[j].name + ' ' +
                        '</a><b class="arrow"></b></li>';
                }
            }

            menuString += '</ul>';
        }

        menuString += '</li>';
    }

    $("#mainMenu").html(menuString);
}

/**
 * 读取code的格式
 * @param data 传入数据
 **/
function readCodeType(data)
{
    data = data.split("_");
    var type = new Array;
    if(data.length == 2){
        if(intval(data[1]) != 0){
            type = {"type": data[0],"id":data[1]};
        }
    }

    return type;
}

function codePage()
{
    var codeFile = getCodeFile();
    mCodeValue = "";

    $.each(codeFile,function(file){
        var data = readCodeType(file);
        if(data.id){
            mCodeName = file;
            mCodeValue = getFile(getCodeDir() + mCodeName + "_code");
            pbox('code_' + data.type);
            return false;
        }
    });
}

/**
 * 转为整数
 * @param val 可为字符串
 **/
function intval(val)
{
    val = parseInt(val);
    return val = isNaN(val) ? 0 : val;
}

function dump(obj)
{
    var data = dumpObj(obj);
    alert(data);
}

/**
 * dump object
 * @param obj 对象
 * @param name 递归使用
 * @param indent 递归使用
 * @param depth 递归使用
 **/
function dumpObj(obj, name, indent, depth)
{
    name = isValue(typeof name) ? name : "";
    indent = isValue(typeof indent) ? indent : "";

    if (depth > 10)
        return indent + name + ": <Maximum Depth Reached>\n";

    if (typeof obj == "object")
    {
        var child = null;
        var output = indent + name + "\n";
        indent += " ";
        for (var item in obj)
        {
            try
            {
                child = obj[item];
            }
            catch (e)
            {
                child = "<Unable to Evaluate>";
            }

            if (typeof child == "object")
                output += dumpObj(child, item, indent, depth + 1);
            else
                output += indent + item + ": " + child + "\n";
        }
        return output;
    }
    else
        return obj;
}

/**
 * 当form按下enter执行的函数
 * @param name 指定的juqery对象
 * @param callbackFunctionName 要执行的函数名
 **/
function formEnter(name,callbackFunctionName)
{
    name += " input";
    $(name).each(function(){
        // var $events = $(this).data("events");

        // if( $events && $events["keydown"] ){
        //     return;
        // }

        // if (this.getAttribute("onkeydown")) {
        //     return;
        // }

        $( this ).keydown(function(event){
            if(event.keyCode==13)
            {
                callbackFunctionName();
            };
        });
    });
}

function t(value)
{
    return $.t(value);
}

function buttonSubmit()
{
    alert('111111');
}

/**
 * 将JSON对象转换为url格式的参数字符串。如：{"id":1,"username"="test"}，转换后为：&id=1&username=test
 * @param param     JSON对象
 * @param key       可选，默认为undefined或者null，json对象的名称
 * @param subIndex  可选，从字符串的第subIndex位置返回
 */
function jsonToUrlParam (param,key,subIndex) {
    var paramStr = "";
    if (param instanceof String || param instanceof Number || param instanceof Boolean
    ) {
        paramStr += "&" + key + "=" + encodeURIComponent(param);
    }
    else {
        $.each(param, function (i) {
            var k = key == null || key === undefined ? i : key + (param instanceof Array ? "[" + i + "]" : "." + i);
            paramStr += '&' + jsonToUrlParam(this, k);
        });
    }
    if (subIndex) return paramStr.substr(subIndex);
    return paramStr;
}
