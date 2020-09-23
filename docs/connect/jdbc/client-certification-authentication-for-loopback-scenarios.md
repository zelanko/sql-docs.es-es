---
description: Autenticación de certificados de cliente para escenarios de bucles invertidos
title: Autenticación de certificados de cliente para escenarios de bucles invertidos | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: peterbae
ms.author: v-hyba
ms.openlocfilehash: bfc8816c30020669918b3632f94e289524097537
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438447"
---
# <a name="client-certificate-authentication-for-loopback-scenarios"></a>Autenticación de certificados de cliente para escenarios de bucles invertidos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Sn SQL Server 2016 se agregó un nuevo procedimiento almacenado llamado sp_execute_external_script (SPEES). Este procedimiento almacenado permite a SQL Server iniciar y ejecutar un script externo fuera de SQL Server, como parte de un trabajo de extensibilidad. Gracias a él, fue posible la compatibilidad con los scripts de R y Python, los cuales tienen bibliotecas que pueden usar un controlador JDBC para conectarse al SQL Server. Aunque el cuadro SQL Servers on Windows (Servidores SQL en Windows) puede usar la autenticación integrada de Windows para autenticar estas conexiones de bucle invertido con las mismas credenciales que el usuario que inició la consulta, SQL Server en Linux no puede hacer lo mismo. Por lo tanto, se está agregando la autenticación de certificados de cliente para permitir que los usuarios se autentiquen con un certificado y una clave.

## <a name="connecting-using-client-certificate-authentication"></a>Conexión mediante la autenticación de certificados de cliente

El controlador JDBC agrega tres propiedades de conexión para esta característica:

* clientCertificate: especifica el certificado que se usará en la autenticación. El controlador JDBC admitirá las extensiones de archivo PFX, PEM, DER y CER.

Formato
```
clientCertificate=<file_location>
``` 
El controlador utiliza un archivo de certificado. Los certificados con el formato PEM, DER y CER requieren el atributo clientKey. La ubicación del archivo puede ser relativa o absoluta.
 
* clientKey: especifica una ubicación de archivo de la clave privada para los certificados PEM, DER y CER especificados por el atributo clientCertificate.

Formato
```
clientKey=<file_location>
```
Especifica la ubicación del archivo de clave privada. En caso de que el archivo de clave privada esté protegido por contraseña, se requiere la palabra clave de contraseña. La ubicación del archivo puede ser relativa o absoluta.

* clientKeyPassword: cadena de contraseña opcional que se proporciona para tener acceso a la clave privada del archivo clientKey.

Esta característica solo se admite oficialmente en escenarios de autenticación de bucle invertido en SQL Server 2019 en Linux y versiones superiores.

## <a name="see-also"></a>Consulte también

[Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
