---
title: Notas de la versión de Microsoft DacFx & sqlpackage | Microsoft Docs
description: Notas de la versión de Microsoft sqlpackage
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: f9fe0558b169acea58bb98a4f9a07267549aa58f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013006"
---
# <a name="sqlpackage-release-notes"></a>notas de la versión de Sqlpackage

**[Descargar la última versión](sqlpackage-download.md)**

## <a name="sqlpackage-181"></a>sqlpackage 18.1

Fecha de publicación: 1 de febrero de 2019  
Compilación 

La versión incluye las siguientes características y correcciones:

- Se agregó compatibilidad para las intercalaciones de UTF8.
- Corrección del rendimiento que se usará el Estimador de cardinalidad heredada para las consultas de ingeniería inversas.
- Habilitar los índices de almacén de columnas no agrupado en las vistas indizadas.
- Se ha corregido un problema de rendimiento de la comparación de esquema importantes cuando se genera una secuencia de comandos.
- Se ha corregido la lógica de detección del desfase esquema para omitir ciertas sesiones de xevent.
- Importación fija de ordenación de las tablas de graph.
- Se ha corregido la exportación de tablas externas con permisos de objeto.
- Mover a .NET Core 2.2 
- Utilice el almacenamiento de seguridad de memoria para la comparación de esquemas en .NET Core.

Esta versión incluye las compilaciones de versión preliminar de multiplataforma de sqlpackage destinadas a .NET Core 2.2, y pueden ejecutar en Mac OS y Linux. Esta versión preliminar tiene los siguientes problemas conocidos:

- No se admiten los colaboradores de compilación e implementación.
- No se admiten archivos de dacpac y bacpac antiguos que utilizan la serialización de datos de json.
- No se puede solucionar .dacpacs que se hace referencia (por ejemplo master.dacpac) debido a problemas con los sistemas de archivos distingue mayúsculas de minúsculas.
  - Una solución consiste en poner en mayúsculas del nombre del archivo de referencia (por ejemplo maestra. BACPAC).
## <a name="sqlpackage-180"></a>sqlpackage 18.0

Fecha de publicación: 24 de octubre de 2018  
Compilación: 15.0.4200.1 

La versión incluye las siguientes características y correcciones:

- Se agregó compatibilidad para el nivel de compatibilidad de base de datos 150.
- Se agregó compatibilidad para instancias administradas.
- Se ha agregado el parámetro de línea de comandos del MaxParallelism para especificar el grado de paralelismo para las operaciones de base de datos.
- Agregar parámetro de línea de comandos AccessToken para especificar un token de autenticación al conectarse a SQL Server.
- Se agregó compatibilidad para tipos de datos BLOB y CLOB secuencia para la importación.
- Ha agregado compatibilidad con UDF escalar opción "INLINE".
- Se ha agregado compatibilidad con la sintaxis 'MERGE' de tabla de gráfico.
- Columna pseudo sin resolver fijo para las tablas de graph.
- Se ha corregido la creación de una base de datos con el archivo optimizado de memoria se usan grupos de tablas optimizadas para memoria.
- Se ha corregido, incluidas las propiedades extendidas en tablas externas.

## <a name="sqlpackage-178"></a>sqlpackage 17.8

Fecha de publicación: 22 de junio de 2018  
Compilación: 14.0.4079.2  

La versión incluye las siguientes correcciones:

- Mejorado los mensajes de error para errores de conexión, incluidos el mensaje de excepción de SqlClient.
- Admite la compresión de índice en los índices de partición única para import/export.
- Se ha corregido un problema de ingeniería inverso para conjuntos de columnas XML con SQL 2017 y versiones posteriores.
- Se ha corregido un problema donde se omitió el scripting en el nivel de compatibilidad 140 para Azure SQL Database.

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

Fecha de publicación: 25 de enero de 2018  
Compilación: 14.0.3917.1

La versión incluye las siguientes correcciones:

- Al importar un bacpac de Azure SQL Database a una instancia local, se han corregido errores debido a 'no se admiten las claves maestras de base de datos sin contraseña en esta versión de SQL Server'.
- Compatibilidad con la intercalación del catálogo de base de datos.
- Se ha corregido un error de la columna pseudo sin resolver para las tablas de graph.
- Se ha agregado el parámetro de línea de comandos del ThreadMaxStackSize analizar TSQL con un gran número de instrucciones anidadas.
- Se ha corregido utilizando el SchemaCompareDataModel con autenticación de SQL para comparar los esquemas.

## <a name="sqlpackage-1740"></a>sqlpackage 17.4.0

Fecha de publicación: 12 de diciembre de 2017  
Compilación: 14.0.3881.1

La versión incluye las siguientes correcciones:

- No se bloquean cuando encuentre un nivel de compatibilidad de base de datos no entiende. En su lugar, se asumirá el más reciente de Azure SQL Database o la plataforma de a nivel local.
- Compatibilidad agregada para 'directiva de retención temporal' en SQL2017 + y Azure SQL Database.
- Se agregó /DiagnosticsFile:"C:\Temp\sqlpackage.log" parámetro de línea de comandos para especificar una ruta de acceso de archivo para guardar la información de diagnóstico.
- Se ha agregado el parámetro de línea de comandos del /Diagnostics para registrar información de diagnóstico en la consola.

