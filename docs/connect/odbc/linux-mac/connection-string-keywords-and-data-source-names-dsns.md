---
title: "Palabras clave de cadena de conexión y origen de datos (DSN) de nombres | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 508fcb62b7cf9ccd78c04b869add7acccb14f258
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connection-string-keywords-and-data-source-names-dsns"></a>Palabras clave de cadena de conexión y nombres de orígenes de datos (DSN)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tema describe cómo puede crear una conexión a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="connection-properties"></a>Propiedades de conexión  
En esta versión de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux o Mac OS, puede usar las palabras clave de conexión siguientes:  
  
||||||  
|-|-|-|-|-|  
|`Addr`|`Address`|`ApplicationIntent`|`AutoTranslate`|`Database`|
|`Driver`|`DSN`|`Encrypt`|`FileDSN`|`MARS_Connection`|  
|`MultiSubnetFailover`|`PWD`|`Server`|`Trusted_Connection`|`TrustServerCertificate`|  
|`UID`|`WSID`|`ColumnEncryption`|`TransparentNetworkIPResolution`||  

> [!IMPORTANT]  
> Al conectarse a una base de datos que usa la creación de reflejo de la base de datos (tiene un asociado de conmutación por error), no especifique el nombre de la base de datos en la cadena de conexión. En su lugar, envíe un **usar** *database_name* comando para conectarse a la base de datos antes de ejecutar las consultas.  
  
Para obtener más información sobre estas palabras clave, consulte la sección ODBC de [Usar palabras clave de cadena de conexión con SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkID=126696).  
  
El valor pasado a la **controlador** palabra clave puede tener uno de los siguientes:  
  
-   El nombre que usó cuando instaló el controlador.

-   La ruta de acceso a la biblioteca de controladores, que se especificó en el archivo .ini de plantilla usado para instalar al controlador.  

Para crear un DSN, cree (si es necesario) y edite el archivo **~/.odbc.ini** (`.odbc.ini` en su directorio particular) para un DSN de usuario solo accesible para el usuario actual, o `/etc/odbc.ini` para un DSN de sistema (privilegios administrativos necesarios). El siguiente es un archivo de ejemplo que muestra las entradas necesarias para mínimo para un DSN:  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

También puede especificar el protocolo y el puerto para conectarse al servidor. Por ejemplo, **Server = tcp:***servername***, 12345**. Tenga en cuenta que es el único protocolo compatible con los controladores de Linux y Mac OS `tcp`.

Para conectarse a una instancia con nombre en un puerto estático, use <b>Server =</b>*servername*,**port_number**. No se puede conectar a un puerto dinámico.  

Como alternativa, puede agregar la información de DSN a un archivo de plantilla y ejecute el siguiente comando para agregarlo al `~/.odbc.ini` :
 - **Odbcinst -i -s -f** *template_file*  
 
Puede comprobar que el controlador funciona mediante el uso de `isql` probar la conexión o puede utilizar este comando:
 - **master.INFORMATION_SCHEMA.TABLES bcp out archivo OutFile.dat -S <server> - U <name> - P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Uso de la capa de sockets seguros (SSL)  
Puede usar capa de Sockets seguros (SSL) para cifrar las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. SSL protege [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombres de usuario y contraseñas a través de la red. SSL también comprueba la identidad del servidor para protegerse de ataques de tipo "Man in the middle" (MITM).  

Al habilitar el cifrado, aumenta la seguridad a expensas del rendimiento.

Para obtener más información, consulte [cifrar conexiones a SQL Server](http://go.microsoft.com/fwlink/?LinkId=220900) y [utilizar el cifrado sin validación](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation).

Con independencia de la configuración de **Encrypt** y **TrustServerCertificate**, siempre se cifran las credenciales de inicio de sesión del servidor (nombre de usuario y contraseña). En la tabla siguiente se muestra el efecto de la configuración de **Encrypt** y **TrustServerCertificate** .  

||**TrustServerCertificate = no**|**TrustServerCertificate = yes**|  
|-|-------------------------------------|------------------------------------|  
|**Cifrar = no**|No se comprueba el certificado de servidor.<br /><br />No se cifran los datos enviados entre cliente y servidor.|No se comprueba el certificado de servidor.<br /><br />No se cifran los datos enviados entre cliente y servidor.|  
|**Cifrar = sí**|Se comprueba el certificado de servidor.<br /><br />Se cifran los datos enviados entre cliente y servidor.<br /><br />El nombre (o dirección IP) en un nombre común del asunto (CN) o nombre alternativo del sujeto (SAN) en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL debe coincidir exactamente con el nombre de servidor (o dirección IP) especificado en la cadena de conexión.|No se comprueba el certificado de servidor.<br /><br />Se cifran los datos enviados entre cliente y servidor.|  

De forma predeterminada, las conexiones cifradas siempre comprueban el certificado del servidor. Sin embargo, si se conecta a un servidor que tenga un certificado autofirmado, agregar el `TrustServerCertificate` opción para omitir la comprobación del certificado con la lista de entidades emisoras de certificados de confianza:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL utiliza la biblioteca OpenSSL. En la siguiente tabla se muestran las versiones mínimas admitidas de OpenSSL y las ubicaciones de almacén de confianza de certificados predeterminadas para cada plataforma:

|Plataforma|Versión mínima de OpenSSL|Ubicación del almacén de confianza de certificados predeterminada|  
|------------|---------------------------|--------------------------------------------|
|Debian 8.71 |1.0.1T|/etc/ssl/certs|
|macOS 10.12|1.0.2K|/usr/local/etc/OpenSSL/certs|
|OS X 10.11|1.0.2J|/usr/local/etc/OpenSSL/certs|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|  
|Red Hat Enterprise Linux 7|1.0.1E|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1I|/etc/ssl/certs|
|Ubuntu 15.10 |1.0.2d|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2g|/etc/ssl/certs|
|Ubuntu 16,10 |1.0.2g|/etc/ssl/certs|
  
También puede especificar el cifrado en la cadena de conexión usando la `Encrypt` cuando se utiliza la opción **SQLDriverConnect** para conectarse.

## <a name="see-also"></a>Vea también  
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)

