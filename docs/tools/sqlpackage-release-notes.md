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
ms.openlocfilehash: c146426a9c325eec721e3289d711d0a00a632e2c
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050857"
---
# <a name="sqlpackage-release-notes"></a>notas de la versión de Sqlpackage

**[Descargar la última versión](sqlpackage-download.md)**

## <a name="sqlpackage-180"></a>sqlpackage 18.0

Fecha de lanzamiento: 24 de octubre de 2018  
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

## <a name="sqlpackage-on-macos-and-linux-001-preview"></a>Sqlpackage en macOS y Linux 0.0.1 (versión preliminar)

Fecha de publicación: 9 de mayo de 2018  
Compilación: 15.0.4057.1

Esta versión contiene la compilación de versión preliminar de multiplataforma de sqlpackage que tenga como destino .NET Core 2.0 y puede ejecutar en Mac OS y Linux. 

Esta versión es una versión preliminar con los siguientes problemas conocidos:

- El parámetro /p:CommandTimeout está codificado en 120.
- No se admiten los colaboradores de compilación e implementación.
  - Se corregirá después de mover a donde se admite System.ComponentModel.Composition.dll .NET Core 2.1.
  - Es necesario controlar las rutas de acceso distingue mayúsculas de minúsculas.
- No se admiten tipos UDT de CLR de SQL, incluidos los tipos UDT de CLR de SQL Server: SqlHierarchyId, SqlGeometry y SqlGeography.
- No se admiten archivos de dacpac y bacpac antiguos que utilizan la serialización de datos de json.
- No se puede solucionar .dacpacs que se hace referencia (por ejemplo master.dacpac) debido a problemas con los sistemas de archivos distingue mayúsculas de minúsculas.
  - Una solución consiste en poner en mayúsculas del nombre del archivo de referencia (por ejemplo maestra. BACPAC).
