---
title: Conectarse a SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aff97d687a4519d2451895772ba33f2a2ec3c4f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-to-sql-server"></a>Conectarse a SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tema describe cómo puede crear una conexión a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="connection-properties"></a>Propiedades de conexión  

Vea [DSN y palabras clave de cadena de conexión y los atributos](../../../connect/odbc/dsn-connection-string-attribute.md) para todas las palabras clave de cadena de conexión y los atributos admitidos en Linux y Mac

> [!IMPORTANT]  
> Al conectarse a una base de datos que usa la creación de reflejo de la base de datos (tiene un asociado de conmutación por error), no especifique el nombre de la base de datos en la cadena de conexión. En su lugar, envíe un **usar** *database_name* comando para conectarse a la base de datos antes de ejecutar las consultas.  
  
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
 - **master.INFORMATION_SCHEMA.TABLES bcp out archivo OutFile.dat -S <server> - U <name> - P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Uso de la capa de sockets seguros (SSL)  
Puede usar capa de Sockets seguros (SSL) para cifrar las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. SSL protege [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombres de usuario y contraseñas a través de la red. SSL también comprueba la identidad del servidor para protegerse de ataques de tipo "Man in the middle" (MITM).  

Al habilitar el cifrado, aumenta la seguridad a expensas del rendimiento.

Para obtener más información, consulte [cifrar conexiones a SQL Server](http://go.microsoft.com/fwlink/?LinkId=220900) y [utilizar el cifrado sin validación](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation).

Con independencia de la configuración de **Encrypt** y **TrustServerCertificate**, siempre se cifran las credenciales de inicio de sesión del servidor (nombre de usuario y contraseña). En la tabla siguiente se muestra el efecto de la configuración de **Encrypt** y **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate = yes**|  
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
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|versión 1.0.2|/usr/local/etc/OpenSSL/certs|
|macOS 10.12|versión 1.0.2|/usr/local/etc/OpenSSL/certs|
|OS X 10.11|versión 1.0.2|/usr/local/etc/OpenSSL/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |versión 1.0.2|/etc/ssl/certs|
|Ubuntu 16,10 |versión 1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |versión 1.0.2|/etc/ssl/certs|
  
También puede especificar el cifrado en la cadena de conexión usando la `Encrypt` cuando se utiliza la opción **SQLDriverConnect** para conectarse.

## <a name="see-also"></a>Vea también  
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)
