---
title: Conectarse a una base de datos SQL de Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 183cd9c749cac8b1af3d97a9830d4d4288fd464f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832480"
---
# <a name="connecting-to-an-azure-sql-database"></a>Conectarse a una base de datos de SQL Azure
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En este tema se describe los problemas cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para conectarse a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Para obtener más información sobre cómo conectarse a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], vea:  
  
-   [SQL Azure base de datos](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [Cómo: conectarse a SQL Azure mediante JDBC](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [Usar SQL Azure en Java](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [Conectarse usando la autenticación de Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Detalles  
 Cuando se conecta a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe conectarse a la base de datos maestra para llamar a **SQLServerDatabaseMetaData.getCatalogs**.  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] no se admite la devolución de todo el conjunto de catálogos de una base de datos de usuario. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases para obtener los catálogos. Consulte la discusión de permisos en [sys.databases (base de datos de SQL Azure)](http://go.microsoft.com/fwlink/?LinkId=217396) comprender **SQLServerDatabaseMetaData.getCatalogs** comportamiento en un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
 Conexiones eliminadas  
 Cuando se conecta a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], un componente de red (por ejemplo, un firewall) pueden terminar las conexiones inactivas tras un período de inactividad. Existen dos tipos de conexiones inactivas en este contexto:  
  
-   Inactiva en la capa de TCP, donde cualquier número de dispositivos de red puede quitar las conexiones.  
  
-   Inactiva por la puerta de enlace de SQL Azure, donde TCP **keepalive** darse mensajes puede estar produciendo (pasando a la conexión no inactiva desde una perspectiva de TCP), pero no tenía una consulta activa en 30 minutos. En este escenario, la puerta de enlace determinará si la conexión TDS está inactiva después de 30 minutos y la finalizará.  
  
 Para evitar que un componente de red elimine las conexiones inactivada, se debe establecer la siguiente configuración del Registro (o su equivalente si no es Windows) en el sistema operativo donde esté cargado el controlador:  
  
|Configuración del registro|Valor recomendado|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ servicios \ Tcpip \ parámetros \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ servicios \ Tcpip \ parámetros \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ servicios \ Tcpip \ parámetros \ TcpMaxDataRetransmissions|10|  
  
 A continuación, debe reiniciar el equipo para que surta efecto la configuración del Registro.  
  
 Para llevar a cabo esta tarea cuando se ejecuta en Windows Azure, cree una tarea de inicio para agregar las claves del Registro.  Por ejemplo, agregue la siguiente tarea de inicio al archivo de definición de servicios:  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 A continuación, agregue un archivo AddKeepAlive.cmd al proyecto. Establezca la configuración "Copy to Output Directory" en Copy always. A continuación se muestra un archivo AddKeepAlive.cmd de ejemplo:  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 Anexar el nombre de servidor al identificador de usuario en la cadena de conexión  
 Antes de la versión 4.0 de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], al conectarse a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], se tenía que anexar el nombre del servidor al identificador de usuario en la cadena de conexión. Por ejemplo, user@servername. A partir de la versión 4.0 de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ya no es necesario anexar @servername al identificador de usuario en la cadena de conexión.  
  
 Usar el cifrado requiere establecer hostNameInCertificate  
 Cuando se conecta a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe especificar **hostNameInCertificate** si especifica **cifrar = true**. (Si es el nombre del servidor en la cadena de conexión *shortName*. *domainName*, establezca el **hostNameInCertificate** propiedad \*. *domainName*.)  
  
 Por ejemplo:  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>Vea también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
