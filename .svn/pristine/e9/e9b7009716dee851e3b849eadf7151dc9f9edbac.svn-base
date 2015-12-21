Set ws = CreateObject("Wscript.Shell")

paramPath = wscript.arguments(0)

svnApp = """" + paramPath  + "update/svn.exe"""
appPath = """" + paramPath  + """"
appData = """" + paramPath  + "data/"""
appExe = """" + paramPath  + "Cowflow.exe"""

wscript.sleep 3000

ws.run svnApp + " cleanup " + appPath,vbhide,true
ws.run svnApp + " revert -R " + appPath,vbhide,true
ws.run svnApp + " up --accept theirs-full " + appPath,vbhide,true

ws.run svnApp + " cleanup " + appData,vbhide,true
ws.run svnApp + " revert -R " + appData,vbhide,true
ws.run svnApp + " up --accept theirs-full " + appData,vbhide,true

ws.run appExe,1
