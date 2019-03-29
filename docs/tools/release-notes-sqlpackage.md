---
title: Notas de la versión de DacFx y SqlPackage | Microsoft Docs
description: Notas de la versión Microsoft sqlpackage.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538781"
---
# <a name="release-notes-for-sqlpackageexe"></a>Notas de la versión de SqlPackage.exe

**[Descargar la última versión](sqlpackage-download.md)**

En este artículo se enumera las características y correcciones entregadas por las versiones publicadas de SqlPackage.exe.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>18.1 sqlpackage

Fecha de la versión: &nbsp; 1 de febrero de 2019  
Compilación: &nbsp; 15.0.4316.1  
Versión preliminar.

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó compatibilidad para las intercalaciones de UTF8. | &nbsp; |
| Habilitar los índices de almacén de columnas no agrupado en una vista indizada. | &nbsp; |
| Mover a .NET Core 2.2. | &nbsp; |
| Utilice el almacenamiento de seguridad de memoria para la comparación de esquemas en .NET Core. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Corrección del rendimiento que se usará el Estimador de cardinalidad heredada para las consultas de ingeniería inversas. | &nbsp; |
| Se ha corregido un problema de rendimiento de la comparación de esquema importantes cuando se genera una secuencia de comandos. | &nbsp; |
| Se ha corregido la lógica de detección del desfase de esquema para omitir ciertas sesiones de eventos extendidos (xevent). | &nbsp; |
| Importación fija de ordenación de las tablas de graph. | &nbsp; |
| Se ha corregido la exportación de tablas externas con permisos de objeto. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

Esta versión incluye las compilaciones de versión preliminar de multiplataforma de sqlpackage que tienen como destino .NET Core 2.2. Puede ejecutar el sqlpackage en macOS y Linux.

| Problema conocido | Detalles |
| :---------- | :------ |
| No se admiten los colaboradores de compilación e implementación. | &nbsp; |
| No se admiten archivos de dacpac y bacpac antiguos que utilizan la serialización de datos de json. | &nbsp; |
| No se puede solucionar .dacpacs que se hace referencia (por ejemplo master.dacpac) debido a problemas con los sistemas de archivos distingue mayúsculas de minúsculas. | Una solución consiste en poner en mayúsculas del nombre del archivo de referencia (por ejemplo maestra. BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

Fecha de lanzamiento: &nbsp; 24 de octubre de 2018  
Compilación: &nbsp; 15.0.4200.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó compatibilidad para el nivel de compatibilidad de base de datos 150. | &nbsp; |
| Se agregó compatibilidad para instancias administradas. | &nbsp; |
| Se ha agregado el parámetro de línea de comandos del MaxParallelism para especificar el grado de paralelismo para las operaciones de base de datos. | &nbsp; |
| Se ha agregado el parámetro de línea de comandos del AccessToken para especificar un token de autenticación al conectarse a SQL Server. | &nbsp; |
| Se agregó compatibilidad para tipos de datos BLOB y CLOB secuencia para la importación. | &nbsp; |
| Ha agregado compatibilidad con UDF escalar opción "INLINE". | &nbsp; |
| Se ha agregado compatibilidad con la sintaxis 'MERGE' de tabla de gráfico. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Columna pseudo sin resolver fijo para las tablas de graph. | &nbsp; |
| Se ha corregido la creación de una base de datos con el archivo optimizado de memoria se usan grupos de tablas optimizadas para memoria. | &nbsp; |
| Se ha corregido, incluidas las propiedades extendidas en tablas externas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

Fecha de publicación: &nbsp; 22 de junio de 2018  
Compilación: &nbsp; 14.0.4079.2

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Mejorado los mensajes de error para errores de conexión, incluidos el mensaje de excepción de SqlClient. | &nbsp; |
| Admite la compresión de índice en los índices de partición única para import/export. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Se ha corregido un problema de ingeniería inverso para conjuntos de columnas XML con SQL 2017 y versiones posteriores. | &nbsp; |
| Se ha corregido un problema donde se omitió el scripting en el nivel de compatibilidad 140 para Azure SQL Database. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

Fecha de lanzamiento: &nbsp; 25 de enero de 2018  
Compilación: &nbsp; 14.0.3917.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Agregado el parámetro de línea de comandos del ThreadMaxStackSize a analizar Transact-SQL con un gran número de instrucciones anidadas. | &nbsp; |
| Compatibilidad con la intercalación del catálogo de base de datos. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Al importar un bacpac de Azure SQL Database a una instancia local, se han corregido errores debido a _claves maestras de base de datos sin la contraseña no se admiten en esta versión de SQL Server_. | &nbsp; |
| Se ha corregido un error de la columna pseudo sin resolver para las tablas de graph. | &nbsp; |
| Se ha corregido utilizando el SchemaCompareDataModel con autenticación de SQL para comparar los esquemas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

Fecha de publicación: &nbsp; 12 de diciembre de 2017  
Compilación: &nbsp; 14.0.3881.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Ha agregado compatibilidad con _directiva de retención temporal_ en SQL 2017 + y Azure SQL Database. | &nbsp; |
| Se agregó /DiagnosticsFile:"C:\Temp\sqlpackage.log" parámetro de línea de comandos para especificar una ruta de acceso de archivo para guardar la información de diagnóstico. | &nbsp; |
| Se ha agregado el parámetro de línea de comandos del /Diagnostics para registrar información de diagnóstico en la consola. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| No se bloquean al encontrar un nivel de compatibilidad de base de datos que no entienda. | En su lugar, se supone que la plataforma más reciente de Azure SQL Database o en el entorno local. |
| &nbsp; | &nbsp; |
