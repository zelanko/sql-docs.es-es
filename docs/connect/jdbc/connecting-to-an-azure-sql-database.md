---
title: Conectarse a una base de datos SQL de Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
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
ms.openlocfilehash: e716ec94db3f37dc51136f55884ac0c9eb33d236
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278746"
---
# <a name="connecting-to-an-azure-sql-database"></a>Conectarse a una base de datos de SQL Azure
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En este artículo se tratan los problemas de uso de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para conectarse a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Para más información sobre la conexión a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], vea:  
  
-   [Base de datos de SQL Azure](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [Cómo conectar a SQL Azure mediante JDBC](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [Usar SQL Azure en Java](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [Conectarse usando la autenticación de Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Detalles  
 Cuando se conecta a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe conectarse a la base de datos maestra para llamar a **SQLServerDatabaseMetaData.getCatalogs**.  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] no es compatible con la devolución de todo el conjunto de catálogos de una base de datos de usuario. **SQLServerDatabaseMetaData.getCatalogs utilice la vista sys.databases para obtener los catálogos. Consulte la discusión de permisos de [sys.databases (base de datos de SQL Azure)](http://go.microsoft.com/fwlink/?LinkId=217396) comprender **SQLServerDatabaseMetaData.getCatalogs** comportamiento en un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
 Conexiones eliminadas  
 Al conectar con una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], un componente de red (como un firewall) puede terminar las conexiones inactivas tras un período de inactividad. Existen dos tipos de conexiones inactivas en este contexto:  
  
-   Inactiva en la capa de TCP, donde cualquier número de dispositivos de red puede quitar las conexiones.  
  
-   Inactiva por la puerta de enlace de SQL Azure, donde pueden darse mensajes **keepalive** de TCP (pasando a no ser una conexión inactiva desde una perspectiva de TCP) y no tener una consulta activa en 30 minutos. En este escenario, la puerta de enlace determinará si la conexión TDS está inactiva después de 30 minutos y la finalizará.  
  
 Para evitar que un componente de red elimine las conexiones inactivada, se debe establecer la siguiente configuración del Registro (o su equivalente si no es Windows) en el sistema operativo donde esté cargado el controlador:  
  
|Configuración del Registro|Valor recomendado|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ Services \ Tcpip \ parámetros \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ Services \ Tcpip \ parámetros \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ sistema \ CurrentControlSet \ Services \ Tcpip \ parámetros \ TcpMaxDataRetransmissions|10|  
  
 Reinicie el equipo para que surta efecto la configuración del Registro.  
  
 Para llevar a cabo esta tarea cuando se ejecuta en Windows Azure, cree una tarea de inicio para agregar las claves del Registro.  Por ejemplo, agregue la siguiente tarea de inicio al archivo de definición de servicios:  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 A continuación, agregue un archivo AddKeepAlive.cmd al proyecto. Establezca la configuración "Copy to Output Directory" en Copy always. A continuación se muestra un archivo AddKeepAlive.cmd de ejemplo:  
  
```bat
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
 Antes de la versión 4.0 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], al conectarse a una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], se tenía que anexar el nombre de servidor al identificador de usuario en la cadena de conexión. Por ejemplo, user@servername. A partir de la versión 4.0 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ya no es necesario anexar @servername al identificador de usuario en la cadena de conexión.  
  
 Usar el cifrado requiere establecer hostNameInCertificate  
 Cuando se conecta a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe especificar **hostNameInCertificate** si especifica **cifrar = true**. (Si es el nombre del servidor en la cadena de conexión *shortName*. *domainName*, establezca el **hostNameInCertificate** propiedad \*. *domainName*.)  
  
 Por ejemplo:  
  
```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>Ver también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
