---
title: "Agrupación de conexiones dependientes del controlador en el controlador ODBC para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67cb0f520c9e75606c7e1ffcae42d20d87a3d9fb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>Agrupación de conexiones dependientes del controlador ODBC para SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] admite [agrupación de conexiones dependientes del controlador](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). En este tema se describe las mejoras realizadas en el controlador ODBC de Microsoft para la agrupación de conexiones dependientes del controlador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows:  
  
-   Independientemente de las propiedades de conexión, las conexiones que usan `SQLDriverConnect` vaya a un grupo independiente de las conexiones que utilizan `SQLConnect`.
- Cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticación y la agrupación de conexiones dependientes del controlador, el controlador no utiliza el contexto de seguridad del usuario de Windows para el subproceso actual para separar las conexiones en el grupo. Es decir, si las conexiones contienen parámetros equivalentes en escenarios de suplantación de Windows con autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y usan las mismas credenciales de autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para conectarse al back-end, varios usuarios de Windows podrían utilizar el mismo grupo de conexiones. Al usar la autenticación de Windows y la agrupación de conexiones dependientes del controlador, el controlador utiliza el contexto de seguridad del usuario de Windows en el subproceso actual con el fin de separar las conexiones del grupo. Es decir, en escenarios de suplantación de Windows, varios usuarios de Windows no compartirán las conexiones aunque utilicen los mismos parámetros.
- Cuando se usa Azure Active Directory y la agrupación de conexiones dependientes del controlador, el controlador también utiliza el valor de autenticación para determinar la pertenencia del grupo de conexiones.
  
-   La característica de agrupación de conexiones dependientes del controlador impide que se devuelva una conexión incorrecta del grupo.  
  
-   Asimismo, reconoce los atributos de conexión específicos del controlador. Por lo tanto, si utiliza una conexión `SQL_COPT_SS_APPLICATION_INTENT` establecido como de solo lectura, dicha conexión obtendrá su propio grupo de conexiones.
-   Establecer el `SQL_COPT_SS_ACCESS_TOKEN` atributo hace que una conexión se agruparán por separado 
  
Si uno de los siguientes id. de atributo de conexión o palabras clave de cadena de conexión difiere entre la cadena de conexión y la cadena de conexión agrupada, el controlador utilizará una conexión agrupada. Sin embargo, se obtendrá un mejor rendimiento si coinciden todos los id. del atributo de conexión o palabras clave de cadena de conexión (para que coincida una conexión en el grupo, el controlador restablece el atributo). El rendimiento será peor, ya que, para restablecer los siguientes parámetros, se requiere una llamada de red adicional.  
  
-    Si dos o más de los siguientes atributos de conexión o palabras clave de conexión son diferentes, no se utilizará una conexión agrupada.  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   Si hay una diferencia en cualquiera de las siguientes palabras clave de conexión entre la cadena de conexión y una cadena de conexión agrupada, no se utilizará una conexión agrupada.  
  
    |Palabra clave|ODBC Driver 13|Controlador ODBC 11|
    |-|-|-|
    |`Address`|Sí|Sí|
    |`AnsiNPW`|Sí|Sí|
    |`App`|Sí|Sí|
    |`ApplicationIntent`|Sí|Sí|  
    |`Authentication`|Sí|No|
    |`ColumnEncryption`|Sí|No|
    |`Database`|Sí|Sí|
    |`Encrypt`|Sí|Sí|  
    |`Failover_Partner`|Sí|Sí|
    |`FailoverPartnerSPN`|Sí|Sí|
    |`MARS_Connection`|Sí|Sí|
    |`Network`|Sí|Sí|
    |`PWD`|Sí|Sí|
    |`Server`|Sí|Sí|
    |`ServerSPN`|Sí|Sí|
    |`TransparentNetworkIPResolution`|Sí|Sí|
    |`Trusted_Connection`|Sí|Sí|
    |`TrustServerCertificate`|Sí|Sí|
    |`UID`|Sí|Sí|
    |`WSID`|Sí|Sí|
    
- Si hay una diferencia en cualquiera de los siguientes atributos de conexión entre la cadena de conexión y una cadena de conexión agrupada, no se utilizará una conexión agrupada.  
  
    |Attribute|ODBC Driver 13|Controlador ODBC 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|Sí|Sí|
    |`SQL_ATTR_PACKET_SIZE`|Sí|Sí|
    |`SQL_COPT_SS_ANSI_NPW`|Sí|Sí|
    |`SQL_COPT_SS_ACCESS_TOKEN`|Sí|No|
    |`SQL_COPT_SS_AUTHENTICATION`|Sí|No|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|Sí|Sí|
    |`SQL_COPT_SS_BCP`|Sí|Sí|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|Sí|No|
    |`SQL_COPT_SS_CONCAT_NULL`|Sí|Sí|
    |`SQL_COPT_SS_ENCRYPT`|Sí|Sí|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|Sí|Sí|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|Sí|Sí|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|Sí|Sí|
    |`SQL_COPT_SS_MARS_ENABLED`|Sí|Sí|
    |`SQL_COPT_SS_OLDPWD`|Sí|Sí|
    |`SQL_COPT_SS_SERVER_SPN`|Sí|Sí|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|Sí|Sí|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|Sí|Sí|
    |`SQL_COPT_SS_TNIR`|Sí|No|
 
-   El controlador puede restablecer y ajustar los siguientes atributos y palabras clave de conexión sin realizar una llamada de red adicional. El controlador restablece estos parámetros para garantizar que la conexión no contenga información incorrecta.  
  
     Estas palabras clave de conexión no se tienen en cuenta cuando el Administrador de controladores intenta hacer coincidir la conexión con una conexión del grupo. Aunque cambie uno de estos parámetros, se puede utilizar una conexión existente. El controlador restablecerá las opciones según proceda. Pueden restablecer estos atributos en el lado del cliente sin realizar una llamada de red adicional.  
  
    |Palabra clave|ODBC Driver 13|Controlador ODBC 11|  
    |-|-|-|  
    |`AutoTranslate`|Sí|Sí|
    |`Description`|Sí|Sí|
    |`MultisubnetFailover`|Sí|Sí|  
    |`QueryLog_On`|Sí|Sí|
    |`QueryLogFile`|Sí|Sí|
    |`QueryLogTime`|Sí|Sí|
    |`Regional`|Sí|Sí|
    |`StatsLog_On`|Sí|Sí|
    |`StatsLogFile`|  Sí|Sí|
  
     Si cambia uno de los siguientes atributos de conexión, se puede reutilizar una conexión existente.  El controlador restablecerá el valor según proceda. El controlador puede restablecer estos atributos en el cliente sin realizar una llamada de red adicional.  
  
    |Attribute|ODBC Driver 13|Controlador ODBC 11|  
    |-|-|-|  
    |Todos los atributos de instrucción|Sí|Sí|
    |`SQL_ATTR_AUTOCOMMIT`|Sí|Sí|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  Sí|Sí|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|Sí|Sí|
    |`SQL_ATTR_LOGIN_TIMEOUT`|Sí|Sí|
    |`SQL_ATTR_ODBC_CURSORS`|  Sí|Sí|
    |`SQL_COPT_SS_PERF_DATA`|Sí|Sí|
    |`SQL_COPT_SS_PERF_DATA_LOG`|Sí|Sí|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| Sí|Sí| 
    |`SQL_COPT_SS_PERF_QUERY`|Sí|Sí|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|Sí|Sí|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  Sí|Sí|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|Sí|Sí|
    |`SQL_COPT_SS_TRANSLATE`|Sí|Sí|
    |`SQL_COPT_SS_USER_DATA`|  Sí|Sí|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|Sí|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
