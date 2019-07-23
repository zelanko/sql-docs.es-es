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
ms.openlocfilehash: f1bbdb044afd8fb4a5ff55d1a9d5fea2b3f14da1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008829"
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

Para conectarse a una instancia con nombre en un puerto estático, use <b>Server=</b>*servername*,**port_number**. No se admite la conexión a un puerto dinámico.  

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
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|1.0.2|/usr/local/etc/openssl/certs|
|macOS 10.12|1.0.2|/usr/local/etc/openssl/certs|
|OS X 10.11|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2|/etc/ssl/certs|
  
También puede especificar el cifrado en la cadena de conexión `Encrypt` mediante la opción al usar **SQLDriverConnect** para conectarse.

## <a name="see-also"></a>Consulte también  
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
