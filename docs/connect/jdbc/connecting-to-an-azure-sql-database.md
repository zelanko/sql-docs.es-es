---
title: Conectarse a una base de datos de Azure SQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f7ecc575fc444a7f834cd8ed84ee340902199b09
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922466"
---
# <a name="connecting-to-an-azure-sql-database"></a>Conectarse a una base de datos de SQL Azure

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se tratan los problemas de uso de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para conectarse a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Para más información sobre la conexión a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], vea:  
  
- [Base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)  
  
- [Cómo conectar a SQL Azure mediante JDBC](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)  

- [Conectarse usando la autenticación de Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Detalles

Al conectarse a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe conectarse a la base de datos maestra para llamar a **SQLServerDatabaseMetaData.getCatalogs**.  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] no es compatible con la devolución de todo el conjunto de catálogos de una base de datos de usuario. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases para obtener los catálogos. Consulte la explicación de los permisos en [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) para entender el comportamiento **SQLServerDatabaseMetaData.getCatalogs** en una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
## <a name="connections-dropped"></a>Conexiones eliminadas

Al conectar con una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], un componente de red (como un firewall) puede terminar las conexiones inactivas tras un período de inactividad. Existen dos tipos de conexiones inactivas en este contexto:  

- Inactiva en la capa de TCP, donde cualquier número de dispositivos de red puede quitar las conexiones.  

- Inactiva por la puerta de enlace de SQL Azure, donde pueden darse mensajes **keepalive** de TCP (pasando a no ser una conexión inactiva desde una perspectiva de TCP) y no tener una consulta activa en 30 minutos. En este escenario, la puerta de enlace determinará si la conexión TDS está inactiva después de 30 minutos y la finalizará.  
  
Para evitar que un componente de red elimine las conexiones inactivada, se debe establecer la siguiente configuración del Registro (o su equivalente si no es Windows) en el sistema operativo donde esté cargado el controlador:  
  
|Configuración del registro|Valor recomendado|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ Parameters \ TcpMaxDataRetransmissions|10|  
  
Reinicie el equipo para que surta efecto la configuración del Registro.  

Para llevar a cabo esta tarea cuando se ejecuta en Azure, cree una tarea de inicio para agregar las claves del Registro.  Por ejemplo, agregue la siguiente tarea de inicio al archivo de definición de servicios:  

```xml
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

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>Anexar el nombre de servidor al identificador de usuario en la cadena de conexión  

Antes de la versión 4.0 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], al conectarse a una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], se tenía que anexar el nombre de servidor al identificador de usuario en la cadena de conexión. Por ejemplo, user@servername. A partir de la versión 4.0 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ya no es necesario anexar @servername al identificador de usuario en la cadena de conexión.  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>El empleo de cifrado exige establecer hostNameInCertificate

Antes de la versión 7.2 de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], al conectarse a una [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], debe especificar **hostNameInCertificate** si especifica **encrypt=true** (si el nombre del servidor de la cadena de conexión es *shortName*.*domainName*, establezca la propiedad **hostNameInCertificate** en \*.*domainName*.). Esta propiedad es opcional a partir de la versión 7.2 del controlador.

Por ejemplo:

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>Consulte también

[Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
