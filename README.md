# Unity CommandLine

## Install
[![NPM](https://nodei.co/npm/com.calci.commandline.png)](https://npmjs.org/package/com.calci.commandline)
- scope : `com.calci`  
- package name : `com.calci.commandline`  

## Editor
the setting for editor is stored at `Assets/Editor Default Resources/CommandLine Setting.asset`.  
also, you can modify the setting in `Project Settings/Command Line`.  
this should not be included in standalone build.  

![image](https://user-images.githubusercontent.com/79823287/135699649-8142430f-d98e-4e6a-b688-71ac26460acb.png)

## Standalone
`Uber\AutoChessFramework.exe --server=true --address=127.0.0.1 --port=29401 --serverPort=29320 --matchHost=127.0.0.1 --matchPortServer=13982 --matchPortClient=12982 --overrideMatchServer=true --width=1600 --height=900 --fullScreen=false`

## Code
```csharp
/// <summary>
/// Parse overriding commandlines.
/// </summary>
private IEnumerator ParseArgument()
{
	if (CommandLineParser.GetBool("overrideMatchServer"))
	{
		matchmakingServerHost = CommandLineParser.GetString("matchHost", "127.0.0.1");
		matchmakingServerPort = CommandLineParser.GetInt("matchPortServer");
			
		matchmakingServerParsed = true;	
	}
	else
	{
		// Download from CDN
		yield return Registry.Get();	
				
		matchmakingServerHost = Registry.Host;
		matchmakingServerPort = Registry.Port + 1000;
					
		ServerLog.Verbose(L("MM Host : ") + matchmakingServerHost);
		ServerLog.Verbose(L("MM Port : ") + matchmakingServerPort);
	}
}
```

## API
API will return default values when there is no valid key.  
You can specify default value for the situation.  

- `CommandLineParser.HasKey`
- `CommandLineParser.GetBool`
- `CommandLineParser.GetString`
- `CommandLineParser.GetInt`
- `CommandLineParser.GetFloat`

