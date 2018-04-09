---
title: Lista de errores corregidos | Documentos de Microsoft
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
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
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: 5187e07d18c6a967ce0a8fadbac370273684c9dc
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2018
---
# <a name="list-of-bugs-fixed"></a>Lista de errores corregidos

Esta página contiene una lista de errores corregidos en cada versión, a partir de [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 del controlador de ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Correcciones de errores en el [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.1 del controlador de ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Corregido el retraso de 1 segundo al llamar a SQLFreeHandle con MARS habilitado y el atributo de conexión "Encrypt = yes"
- Corregido un error error 22003 en SQLGetData cuando el tamaño del búfer transferido en es menor, a continuación, los datos recuperados (Windows)
- Corregido mensajes de error de AAL truncados
- Se corrige un error poco frecuente en Windows de 32 bits al convertir de flotante el número de punto en un entero
- Se corrigió un problema donde insertar doble en un campo decimal con Always Encrypted en haría ningún error de truncamiento de datos de retorno
- Rol fijo de una advertencia en el instalador de Mac OS
- Envío incorrecto estado fijo para SQL Server durante el intento de recuperación de la sesión cuando se habilitan resistencia de conexión tanto la agrupación de conexiones, haciendo que la sesión de ser eliminados por el servidor

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Correcciones de errores en el [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 del controlador de ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Se ha corregido un error que cuando se utiliza la autenticación Kerberos, podría producirse un error de inserción masiva con error de "acceso denegado"
- Quitar solución a un error de unixODBC presente en la versión inferior a 2.3.1 (controlador duplica los tamaños de ciertos búferes pasados a unixODBC)
- Fija la resistencia de conexión (reconexión) hanging al usar ColumnEncryption = habilitado
- Corregido los errores de creación de DSN, donde cuando con "Autenticación de Active Directory interactivo" opción autenticación de Azure ventana dejen de responder (Windows)
- Corregido un bloqueo excepcional durante el cierre ODBC cuando se habilita la ejecución asincrónica (se produjo al borrar el identificador de conexión)
- Se corrigió un problema donde controlador SQL produjo alto consumo de CPU al ejecutar los procedimientos almacenados de tiempo
- Fijo imposibilidad de recuperar datos de una columna varbinary (max) cifrados sin conversión
- Se solucionó un problema donde después un varchar (max) null columna cifrada se captura mediante SQLGetData() en un cursor estático, la siguiente columna se también anula incluso cuando tiene datos
- Se corrigió un problema con la captura de campo varbinary (max) con Always Encrypted en
- Se solucionó un problema de setlocale() no funciona con Always Encrypted
- Se ha corregido un problema con SQLDescribeParam() devolver error cuando se llama en el parámetro de procedimiento almacenado de tipo XML con Always Encrypted en
- Caracteres de subrayado fijos escape no funciona en SQLTables
- Se ha corregido un error donde se truncan los datos hebreos (varchar) cuando se devuelve como caracteres anchos en Linux
- Se corrigió un problema con una consulta con codificación de Shift-JIS char o varchar de aplicación de UTF-8
- Se ha corregido el error que llamar a SQLGetInfo con el parámetro SQL_DRIVER_NAME devuelve el nombre de archivo de estilo de Linux en Mac OS
- Se corrigió un problema donde cargar los datos de caracteres de Windows-1252, con entradas archivos mayor que 32k bytes en columnas VARCHAR mediante la utilidad BCP se crearán en errores
