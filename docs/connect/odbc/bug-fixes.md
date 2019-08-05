---
title: Lista de errores corregidos | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 9aba2495e5f4661c7c042125608f34d577cddfe3
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702809"
---
# <a name="list-of-bugs-fixed"></a>Lista de errores corregidos

Esta página contiene una lista de errores corregidos en cada versión, a [!INCLUDE[msCoName](../../includes/msconame_md.md)] partir de ODBC driver 17 for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-174-for-includessnoversionincludesssnoversion-mdmd"></a>Correcciones de errores [!INCLUDE[msCoName](../../includes/msconame_md.md)] en el controlador ODBC 17,4 para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Corrección de bloqueo intermitente cuando se habilitan conjuntos de resultados activos múltiples (MARS)
- Corrección de la resistencia de conexión bloqueada cuando está habilitada la notificación asincrónica
- Corregir el bloqueo al recuperar registros de diagnóstico para intentos de conexión multiproceso
- Corrección de ' cifrado no admitido ' tras la reconexión después de llamar a SQLGetInfo () con SQL_USER_NAME y SQL_DATA_SOURCE_READ_ONLY
- Corregir el error de inicialización COM durante la autenticación interactiva de Azure Active Directory
- Corrección de SQLGetData () para datos UTF8 de varios bytes
- Corregir la recuperación de la longitud de las columnas sql_variant mediante SQLGetData ()
- Corregir la importación de columnas sql_variant que contienen más de 7992 bytes mediante BCP
- Corregir el envío de la codificación correcta al servidor para datos de caracteres estrechos

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd"></a>Correcciones de errores [!INCLUDE[msCoName](../../includes/msconame_md.md)] en el controlador ODBC 17,3 para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Identificador de evento de notificación de envío TCP corregido
- Problema de redefinición corregido de enumeración _SQL_FILESTREAM_DESIRED_ACCESS en el archivo de encabezado msodbcsql. h
- Se corrigió el ACCESS_TOKEN que falta y la definición relacionada con la autenticación en el archivo de encabezado msodbcsql. h para Linux

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd"></a>Correcciones de errores [!INCLUDE[msCoName](../../includes/msconame_md.md)] en el controlador ODBC 17,2 para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Se corrigió un mensaje de error acerca de la autenticación de Azure Active Directory
- Detección de codificación fija cuando las variables de entorno de la configuración regional se establecen de manera diferente
- Se corrigió un bloqueo al desconectarse con la recuperación de la conexión en curso.
- Detección corregida de la vida de la conexión
- Se corrigió la detección incorrecta de los sockets cerrados
- Se corrigió una espera infinita al intentar liberar un identificador de instrucción durante la recuperación con errores.
- Se corrigió el comportamiento incorrecto de la desinstalación cuando se instalan las versiones 13 y 17 en Windows
- Comportamiento de descifrado fijo en la plataforma de Windows anterior (Windows 7, 8 y Server 2012)
- Se corrigió un problema de caché al usar la autenticación ADAL en Windows
- Se corrigió un problema que bloqueaba y sobrescribe los registros de seguimiento en Windows

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd"></a>Correcciones de errores [!INCLUDE[msCoName](../../includes/msconame_md.md)] en el controlador ODBC 17,1 para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Retraso de 1 segundo fijo al llamar a SQLFreeHandle con MARS habilitado y el atributo de conexión "Encrypt = Yes"
- Se corrigió un error 22003 al bloquearse en SQLGetData cuando el tamaño del búfer pasado es más pequeño que los datos que se recuperan (Windows)
- Mensajes de error de ADAL truncados corregidos
- Se corrigió un error poco frecuente en Windows de 32 bits al convertir un número de punto flotante en un entero.
- Se corrigió un problema que hacía que la inserción de Double en el campo decimal con Always Encrypted activado devolvería un error de truncamiento de datos
- Se corrigió una advertencia en el instalador de MacOS
- Se corrigió el envío de un estado incorrecto al SQL Server durante el intento de recuperación de la sesión cuando se habilitan la resistencia de la conexión y la agrupación de conexiones, lo que provoca que el servidor Quite la sesión.

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd"></a>Correcciones de errores [!INCLUDE[msCoName](../../includes/msconame_md.md)] en el controlador ODBC 17 para[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

- Se ha corregido un error por el que al usar la autenticación Kerberos, Bulk Insert podía producir el error "acceso denegado"
- Se ha quitado la solución alternativa para un error unixODBC presente en la versión siguiente 2.3.1 (el controlador ha duplicado los tamaños de ciertos búferes pasados a unixODBC)
- Corrección de resistencia de conexión fija (reconexión) cuando se usa ColumnEncryption = Enabled
- Error de creación de DSN corregido, donde cuando se usa la opción "Active Directory autenticación interactiva", la ventana de autenticación de Azure podría dejar de responder (Windows)
- Se corrigió un bloqueo inusual durante el cierre de ODBC cuando la ejecución asincrónica está habilitada (se produjo al borrar el identificador de conexión)
- Se corrigió un problema en el que el controlador de SQL provocó un alto consumo de CPU al ejecutar procedimientos almacenados largos.
- No se ha corregido la incapacidad de recuperar datos en una columna varbinary (Max) cifrada sin conversión
- Se corrigió un problema por el que, después de que se capturase una columna cifrada VARCHAR (Max) null con SQLGetData () en un cursor estático, la columna siguiente también se ha null aunque tenga datos
- Se corrigió un problema con la captura del campo varbinary (Max) con Always Encrypted activado
- Se corrigió un problema de setlocale () que no funciona con Always Encrypted
- Se corrigió un problema con SQLDescribeParam () que devolvía un error al llamarlo en un parámetro de procedimiento almacenado de tipo XML con Always Encrypted activado
- Carácter de subrayado de escape fijo no funcional en SQLTables
- Se corrigió un error en el que los datos en Hebreo (varchar) se truncan cuando se devuelven como caracteres anchos en Linux.
- Se corrigió un problema con la consulta de la aplicación Shift-JIS codificación CHAR/VARCHAR desde la aplicación UTF-8
- Se corrigió el error en el que al llamar a SQLGetInfo con el parámetro SQL_DRIVER_NAME se devolvió un nombre de archivo de estilo Linux en MacOS
- Se ha corregido un problema en el que la carga de datos de caracteres de Windows-1252, con archivos de entrada de más de 32 000 bytes en columnas VARCHAR mediante la utilidad BCP daría lugar a errores
