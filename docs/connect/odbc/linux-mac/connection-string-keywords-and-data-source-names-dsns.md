---
title: Conectarse a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702802"
---
# <a name="connecting-to-sql-server"></a>Conectarse a SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este tema se describe cómo crear una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Propiedades de conexión  

Consulte [palabras clave y atributos de cadena de conexión y DSN](../../../connect/odbc/dsn-connection-string-attribute.md) para todas las palabras clave y atributos de cadena de conexión admitidos en Linux y Mac

> [!IMPORTANT]  
> Al conectarse a una base de datos que usa la creación de reflejo de la base de datos (tiene un asociado de conmutación por error), no especifique el nombre de la base de datos en la cadena de conexión. En su lugar, envíe un comando **use**_database_name_ para conectarse a la base de datos antes de ejecutar las consultas.  
  
El valor que se pasa a la palabra clave **driver** puede ser uno de los siguientes:  
  
-   El nombre que usó cuando instaló el controlador.

-   La ruta de acceso a la biblioteca del controlador, que se especificó en el archivo .ini de plantilla utilizado para instalar el controlador.  

Para crear un DSN, cree (si es necesario) y edite el archivo **~/.Odbc.ini** (`.odbc.ini` en el directorio particular) de un DSN de usuario solo accesible para el usuario `/etc/odbc.ini` actual o para un DSN del sistema (se requieren privilegios administrativos). A continuación se muestra un archivo de ejemplo que muestra las entradas requeridas para un DSN:  

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

También puede especificar el protocolo y el puerto para conectarse al servidor. Por ejemplo, **Server = TCP:** _ServerName_ **, 12345**. Tenga en cuenta que el único protocolo compatible con los controladores de Linux `tcp`y MacOS es.

Para conectarse a una instancia con nombre en un puerto estático, use <b>Server=</b>*servername*,**port_number**. No se admite la conexión a un puerto dinámico antes de la versión 17.4.

De forma alternativa, puede agregar la información de DSN a un archivo de plantilla y ejecutar el siguiente comando para agregarlo a `~/.odbc.ini`:
 - **odbcinst -i -s -f** _template_file_  
 
Puede comprobar que el controlador funciona `isql` mediante para probar la conexión, o puede usar este comando:
 - **BCP Master. INFORMATION_SCHEMA. Tables out. dat-S <server> -U <name> -P<password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Uso de la capa de sockets seguros (SSL)  
Puede usar SSL para cifrar las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Este protocolo protege los nombres de usuario y las contraseñas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través de la red. SSL también comprueba la identidad del servidor para protegerse de ataques de tipo "Man in the middle" (MITM).  

Al habilitar el cifrado, aumenta la seguridad a expensas del rendimiento.

Para obtener más información, vea [cifrar conexiones a SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) y [usar el cifrado sin validación](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Con independencia de la configuración de **Encrypt** y **TrustServerCertificate**, siempre se cifran las credenciales de inicio de sesión del servidor (nombre de usuario y contraseña). En la tabla siguiente se muestra el efecto de la configuración de **Encrypt** y **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|No se comprueba el certificado de servidor.<br /><br />No se cifran los datos enviados entre cliente y servidor.|No se comprueba el certificado de servidor.<br /><br />No se cifran los datos enviados entre cliente y servidor.|  
|**Encrypt=yes**|Se comprueba el certificado de servidor.<br /><br />Se cifran los datos enviados entre cliente y servidor.<br /><br />El nombre (o la dirección IP) de un nombre común (CN) del sujeto o el nombre alternativo del sujeto (SAN) de un certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe coincidir exactamente con el nombre (o la dirección IP) del servidor especificado en la cadena de conexión.|No se comprueba el certificado de servidor.<br /><br />Se cifran los datos enviados entre cliente y servidor.|  

De forma predeterminada, las conexiones cifradas siempre comprueban el certificado del servidor. Sin embargo, si se conecta a un servidor que tiene un certificado autofirmado, agregue también `TrustServerCertificate` la opción para omitir la comprobación del certificado con respecto a la lista de entidades emisoras de certificados de confianza:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL utiliza la biblioteca OpenSSL. En la siguiente tabla se muestran las versiones mínimas admitidas de OpenSSL y las ubicaciones de almacén de confianza de certificados predeterminadas para cada plataforma:

|Plataforma|Versión mínima de OpenSSL|Ubicación del almacén de confianza de certificados predeterminada|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10,11, macOS 10,12, 10,13, 10,14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

También puede especificar el cifrado en la cadena de conexión `Encrypt` mediante la opción al usar **SQLDriverConnect** para conectarse.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>Ajuste de la configuración Keep-Alive de TCP

A partir del controlador ODBC 17,4, la frecuencia con la que el controlador envía paquetes Keep-Alive y los retransmite cuando no se recibe una respuesta es configurable.
Para configurar, agregue la siguiente configuración a la sección del controlador en `odbcinst.ini`, o la sección del DSN en. `odbc.ini` Al conectarse con un DSN, el controlador usará la configuración de la sección del DSN, si está presente; de lo contrario, o si solo se conecta con una cadena de conexión, usará la configuración de la sección del `odbcinst.ini`controlador en. Si el valor no está presente en ninguna ubicación, el controlador utiliza el valor predeterminado.

- `KeepAlive=<integer>`controla la frecuencia con la que TCP intenta comprobar que una conexión inactiva sigue intacta mediante el envío de un paquete Keep-Alive. El valor predeterminado es **treinta** segundos.

- `KeepAliveInterval=<integer>`determina el intervalo que separa las retransmisiones Keep-Alive hasta que se reciba una respuesta.  El valor predeterminado es **1** segundo.


## <a name="see-also"></a>Consulte también  
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
