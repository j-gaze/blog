
## JIRA 

```python
	from jira import JIRA

	options = {
		"server": "https://jira.address/",
		"basic_auth": ("USER", "PASSWORD"),
		"verify": False
	}
	jira = JIRA(options)
```

```bash
python -m pip install --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=filespythonhosted.org --proxy=https://GF2GAZE:Kn0w1ed9e&*7@140.100.200.9:8080 jira
python -m pip install --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=filespythonhosted.org --proxy=https://GF2XXXX:PASSWORD@140.100.200.9:8080 jira
```

In url password we need set for special chars using below notation 
>	https://de.wikipedia.org/wiki/URL-Encoding
```
 ␣	!	"	#	$	%	&	'	(	)	*	+	,	-	.	/	:	;	<	=	>	?	@	[	\	]	{	|	}
%20	%21	%22	%23	%24	%25	%26	%27	%28	%29	%2A	%2B	%2C	%2D	%2E	%2F	%3A	%3B	%3C	%3D	%3E	%3F	%40	%5B	%5C	%5D	%7B	%7C	%7D
```

In windows we need configure PIP
> C:\Apps\pip\pip.ini
> C:\Users\gf2gaze\AppData\Roaming\pip

### pip.ini
```ini
[global]
trusted-host = 	pypi.python.org
		pypi.org
		files.pythonhosted.org
```        	

	
Install JIRA package
```bash
python -m pip install --user jira --proxy=https://GF2GAZE:Kn0w1ed9e%26%2A7@140.100.200.9:8080

python -m pip install --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=files.pythonhosted.org --proxy=https://USER:PASSWORD@IP.IP.IP.IP:8080

python -m pip install --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=files.pythonhosted.org --proxy=https://GF2GAZE:Proces%40%232@140.100.200.9:8080 jira
```

