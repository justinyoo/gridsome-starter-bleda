---
title: "Configuration Encryptor 개발 후기"
date: "2014-04-26"
slug: reviewing-configuration-encryptor
description: ""
author: Justin-Yoo
tags:
- encryption
- decryption
fullscreen: true
cover: https://sa0blogs.blob.core.windows.net/justinchronicles/2014/04/encryption.jpg
---

현재 근무하는 회사의 본사가 미국에 있다보니 [SOX Compliance](http://en.wikipedia.org/wiki/Sarbanes%E2%80%93Oxley_Act)를 모든 어플리케이션에 적용중이다. 따라서, 모든 어플리케이션의 `App.config` 파일과 `Web.config` 파일에 포함되어 있는 보안상 민감한 부분 – `connectionstrings` 섹션과 `appSettings` 섹션을 포함한 여러 부분에 대해 암호화를 해야 하는 상황.

그래서, 하나 만들어 봤다. 윈도우 서버마다 있는 고유의 Machine Key를 이용하여 암호화를 진행하는 것이 바로 그것.

- 리포지토리 URL: [https://github.com/aliencube/Configuration-Encryptor](https://github.com/aliencube/Configuration-Encryptor)
- 다운로드 URL: [http://github.aliencube.org/Configuration-Encryptor/downloads/ConfigurationEncryptor-1.0.0.0.zip](http://github.aliencube.org/Configuration-Encryptor/downloads/ConfigurationEncryptor-1.0.0.0.zip)

닷넷 프레임웍에서 자체적으로 제공하는 Configuration 파일의 암호화 방식은 두가지가 있다. 하나는 `DataProtectionConfigurationProvider`이고 다른 하나는 `RsaProtectedConfigurationProvider`인데, 전자는 Symmetric 암호화를, 후자는 Asymmetric 암호화를 지원한다.[1](#fn-136-1) 이 둘의 차이는:

- `DataProtectionConfigurationProvider`는 서버 고유의 Machine Key를 이용하여 암호화를 하므로 한 서버에서 암호화를 하면 다른 서버에서는 해당 암호화된 파일을 복호화할 수 없다. 반면 `RsaProtectedConfigurationProvider`는 비대칭 키를 이용하기 때문에 여러 서버에서 동일한 키만 갖고 있다면 복호화가 가능하다.
- `DataProtectionConfigurationProvider`는 속도가 빠른 반면, `RsaProtectedConfigurationProvider`는 상대적으로 살짝 속도가 느리다.

위와 같은 장단점 때문에 `RsaProtectedConfigurationProvider`는 서버 팜과 같은 분산 서버 환경에서 동일한 환경을 사용해야 할 경우에 유리하고, `DataProtectionConfigurationProvider`는 한 서버에만 설치하여 사용할 경우에 유리하다.

이번에 개발한 **Configuration Encryptor**를 사용하여 암호화를 진행하게 되면

```xml
<connectionStrings>
    <add name="ConsoleAppContext" connectionString="Data Source=ConsoleAppDbServer;Initial Catalog=ConsoleAppDatabade;User ID=username;Password=pa$$w0rd" />
</connectionStrings>
```

이랬던 `connectionStrings` 섹션이

```bat
AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAUgN5Ngk2H0OrwQq8yD1B0AQAAAACAAAAAAAQZgAAAAEAACAAAABJjctPr78C+dCw1pEiljubWRzpf0lbSwBbvWWZFZKJYAAAAAAOgAAAAAIAACAAAABY09qleOcAvFQsmF7UmE0TgXNQIuIrbikXY2dJzX2qApABAABEIqnEFPm8UpHd3FoUnM5dqFCYFAabr1ny2p77ZpeTGm/4ChabBHf8T8lHN4ciOYqz3Krg30R+dvrgNgTtX9GmxWnjOEkgUQ29TP5Sgi94r1mGTTIJzfL3EL9lp5Y6QKNMQ9nxRvZkFkQWiQVWsqYc5h87gi3ak0RbKXN8Lcjaoe2Tl9hQCNwlbphjh6WRUDOyUo5J86rP9aShmpuRFDgKxoNFG+f0wism2iRw19Paein4HZroHgvYvCZDAE0sp96Efd7J/K12iPmtI62AQT7eEcw6gfAK8k0F1SZMQpQmwpxp1953ZPM2mYgNYNagzKORYNcGKbU8UifSs/VAf8yw8J5l/tIARN8oO/MB+0XZDFdTnI6JeZjNiRGtMqsO62n3BYp4nHdlDEVX/bJhJBIsmcDxZ4Tm/sRTyFiMRGfiEIBWdTOnle5n/doWdysGmSoDc4BC2NAUyEaYYcI/aWpcZolKFepMyG8/naG4dNplpBXvr19N3KE1+MczPSQoXQNyYCQnea2R/zKn7FWAoOlmQAAAAA/wU3ZEcbzZ1xwDebZnrWBLTSKUV5sNYL+f7Ab7x42CW7lAzJqERwwC/w8yhtt+DmcH0uaHkr7im3uuAhLf6FM= 
```

이렇게 암호화가 된다. 닷넷 프레임웍에서 알아서 다 복호화를 해주기 때문에 실제로 해당 어플리케이션에서 이 암호화된 파일을 굳이 따로 복호화 할 필요 없이 그냥 평소에 쓰던 대로 쓰면 된다.

참 쉽죠?

* * *

2. [Encrypting Configuration Data](http://msdn.microsoft.com/en-us/library/ff664594(v=pandp.50).aspx) [↩](#fnref-136-1)
