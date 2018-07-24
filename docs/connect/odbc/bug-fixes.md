---
title: Lista de errores corregidos | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 3b5969a723b230139b9466f75569375f97a0d7b0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2018
ms.locfileid: "37946909"
---
# <a name="list-of-bugs-fixed"></a>Lista de errores corregidos

Esta página contiene una lista de errores corregidos en cada versión, empezando por [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversionmdmd"></a>Correcciones de errores en el [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.2 del controlador de ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Se ha corregido un mensaje de error acerca de la autenticación de Azure Active Directory
- Detección de codificación fija cuando se establecen las variables de entorno de configuración regional de forma diferente
- Fijo un bloqueo tras desconectar con recuperación de la conexión en curso
- Detección fija de vida de la conexión
- Ha corregido la detección incorrecta de sockets cerrados
- Se ha corregido una espera infinita al intentar liberar un identificador de instrucción durante la recuperación con error
- Se ha corregido el comportamiento de desinstalación incorrecto cuando se instalan ambas versiones 13 y 17 en Windows
- Comportamiento de descifrado fijo en la plataforma anterior de Windows (Windows 7, 8 y Server 2012)
- Se ha corregido un problema de la caché cuando se usa la autenticación de ADAL en Windows
- Se corrigió un problema que era el bloqueo y sobrescribir el seguimiento de los registros en Windows

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Correcciones de errores en el [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.1 de controlador ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Se ha corregido el retraso de 1 segundo cuando se llama a SQLFreeHandle teniendo MARS habilitado y el atributo de conexión "Encrypt = yes"
- Se ha corregido un bloqueo de error 22003 en SQLGetData cuando el tamaño del búfer pasado es menor, a continuación, los datos recuperados (Windows)
- Se ha corregido los mensajes de error ADAL truncados
- Se ha corregido un error poco frecuente en Windows de 32 bits al convertir de flotante el número de punto en un entero
- Se ha corregido un problema donde insertar dobles en el campo decimal con Always Encrypted en devolvería el error de truncamiento de datos
- Se ha corregido una advertencia en el instalador de Mac OS
- Se ha corregido el envío de un estado incorrecto a SQL Server durante el intento de recuperación de sesión cuando resistencia de conexión y agrupación de conexiones ambas están habilitadas, provocando la sesión que se puede quitar el servidor

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Correcciones de errores en el [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Se ha corregido un error que cuando se usa la autenticación Kerberos, podría producirse un error de inserción masiva con el error "acceso denegado"
- Quitado solución a un error de unixODBC presente en la versión siguiente 2.3.1 (controlador duplica el tamaño de algunos búferes pasados a unixODBC)
- Se ha corregido la resistencia de conexión (reconexión) que se bloquea cuando se usa ColumnEncryption = habilitado
- Se ha corregido error de creación de DSN, donde cuando con "Autenticación interactiva de Active Directory" la opción autenticación de Azure ventana dejen de responder (Windows)
- Se ha corregido un bloqueo excepcional durante el cierre ODBC cuando se habilita la ejecución asincrónica (se produjo al borrar el identificador de conexión)
- Se corrigió un problema donde el controlador de SQL provocó elevado consumo de CPU al ejecutar procedimientos almacenados larga
- Se corrigió la incapacidad para recuperar datos de una columna varbinary (max) cifrada sin conversión
- Se ha corregido un problema donde un varchar de null (max) después de la columna cifrada se captura mediante SQLGetData() en un cursor estático, la siguiente columna se también anula incluso si tiene datos
- Se corrigió un problema con la captura campo varbinary (max) con Always Encrypted en
- Se ha corregido un problema de setlocale() no funciona con Always Encrypted
- Se ha corregido un problema con SQLDescribeParam() devolver errores cuando se llama en el parámetro de procedimiento almacenado de tipo XML con Always Encrypted en
- Se ha corregido el escape caracteres de subrayado no funciona en SQLTables
- Se ha corregido un error donde se truncan los datos hebreos (varchar) cuando se devuelve como caracteres anchos en Linux
- Se corrigió un problema con una consulta a char o varchar de Shift-JIS codificado en UTF-8 aplicación
- Se ha corregido el error donde llamando a SQLGetInfo con parámetro SQL_DRIVER_NAME devuelve el nombre de archivo basado en Linux en MacOS
- Se ha corregido un problema donde archivos mayor que 32k bytes en columnas VARCHAR con la utilidad BCP daría lugar a errores al cargar datos de caracteres de Windows-1252, mediante la entrada
