---
title: Notas de la versión de DacFx y SqlPackage | Microsoft Docs
description: Notas de la versión de sqlpackage de Microsoft.
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 7fb220f8a5a33d33e2ee9177efd9fe2f713b7439
ms.sourcegitcommit: 243925311cc952dd455faea3c1156e980959d6de
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70774178"
---
# <a name="release-notes-for-sqlpackageexe"></a>Notas de la versión de SqlPackage.exe

**[Descargar la última versión](sqlpackage-download.md)**

En este artículo se enumeran las características y correcciones que ofrecen las versiones publicadas de SqlPackage.exe.

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="183-sqlpackage"></a>18.3 sqlpackage

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar
|:---|:---|:---|:---|:---|
|Windows|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2102893)|6 de septiembre de 2019|18,3|15.0.4532.1|
|macOS .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102894)|6 de septiembre de 2019| 18,3|15.0.4532.1|
|Linux .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102978)|6 de septiembre de 2019| 18,3|15.0.4532.1|
|Windows .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2102979)|6 de septiembre de 2019| 18,3|15.0.4532.1|

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Azure SQL Data Warehouse (versión preliminar) | Agregue compatibilidad para implementar en Azure SQL Data Warehouse. | 
| Implementación | Agregue el parámetro/p: DatabaseLockTimeout = (INT32 ' 60 ') a sqlpackage. | 
| Implementación | Agregue el parámetro/p: LongRunningCommandTimeout = (INT32) a sqlpackage. |
| Exportar/extraer | Agregue el parámetro/p: TempDirectoryForTableData = (STRING) a sqlpackage. |
| Implementación | Permite que los colaboradores de implementación se carguen desde ubicaciones adicionales. Los colaboradores de implementación se cargarán desde el mismo directorio que el archivo. dacpac de destino que se está implementando, el directorio de extensiones en relación con el binario sqlpackage. exe y el parámetro/p: AdditionalDeploymentContributorPaths = (cadena) agregado a sqlpackage donde se pueden especificar ubicaciones de directorio adicionales. |
| Implementación | Agregar compatibilidad para OPTIMIZE_FOR_SEQUENTIAL_KEY. |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Implementación | Corrija para omitir los índices automáticos de modo que no se quiten en la implementación. | 
| Always Encrypted | Corrección para el control de las columnas de Always Encrypted VARCHAR. | 
| Compilación e implementación | Corrija para resolver el método Nodes () para los conjuntos de columnas XML.| 
| ScriptDom | Corrija los casos adicionales en los que la cadena ' URL ' se interprete como un token de nivel superior. | 
| Gráfico | Corrección de TSQL generada para las referencias a pseudo columnas en restricciones.  | 
| Exportar | Genere contraseñas aleatorias que cumplan los requisitos de complejidad. | 
| Implementación | Corrección para respetar los tiempos de espera de comandos al recuperar restricciones. | 
| .NET Core (versión preliminar) | Corrija el registro de diagnóstico en un archivo. | 
| .NET Core (versión preliminar) | Use el streaming para exportar datos de tablas para admitir tablas grandes. | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>sqlpackage 18.2

|Plataforma|Descargar|Fecha de la versión|Versión|Compilar
|:---|:---|:---|:---|:---|
|Windows|[Instalador MSI](https://go.microsoft.com/fwlink/?linkid=2087429)|15 de abril de 2019|18.2|15.0.4384.2|
|macOS .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2087247)|15 de abril de 2019 | 18.2 |15.0.4384.2|
|Linux .NET Core (versión preliminar)|[archivo zip](https://go.microsoft.com/fwlink/?linkid=2087431)|15 de abril de 2019 | 18.2 |15.0.4384.2|

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Agregue compatibilidad con la tabla de grafos para las restricciones perimetrales y las cláusulas de restricciones perimetrales. | &nbsp; |
| Regla de validación de modelo habilitada para admitir 32 columnas de claves de índice para SQL Server 2016 y superiores. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Se corrigió la ingeniería inversa de una base de datos RTM de SQL Server 2016 debido a una sugerencia de consulta no compatible que se está utilizando. | &nbsp; |
| Se corrigió el orden de implementación de las instrucciones de alteración de cierre automático para que se produzcan antes de crear instrucciones de grupo de archivos. | &nbsp; |
| Se corrigió la regresión de análisis de ScriptDom donde la cadena "URL" se interpretaba como un token de nivel superior. | &nbsp; |
| Se corrigió una excepción de referencia nula al analizar una instrucción de índice de adición de tabla de alteración. | &nbsp; |
| Se corrigió la comparación de esquemas para las columnas calculadas persistentes que aceptan valores NULL que siempre se muestran diferentes.| &nbsp; |
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

Fecha de la versión: &nbsp; 1 de febrero de 2019  
Compilación: &nbsp; 15.0.4316.1  
Versión preliminar.

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó compatibilidad con intercalaciones UTF8. | &nbsp; |
| Se habilitaron los índices de almacén de columnas no en clúster en una vista indexada. | &nbsp; |
| Se movió a .NET Core 2.2. | &nbsp; |
| Utilice el almacenamiento con copia de seguridad de memoria para la comparación de esquemas en .NET Core. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Corrección de rendimiento para utilizar el estimador de cardinalidad heredado para consultas de ingeniería inversa. | &nbsp; |
| Se corrigió un problema de rendimiento de comparación de esquema significativo al generar un script. | &nbsp; |
| Se corrigió la lógica de detección de desviación del esquema para ignorar ciertas sesiones de evento extendido (xevent). | &nbsp; |
| Se corrigió el orden de importación para las tablas de grafos. | &nbsp; |
| Se corrigió la exportación de tablas externas con permisos de objeto. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

Esta versión incluye las compilaciones de versión preliminar multiplataforma de sqlpackage que tienen como destino .NET Core 2.2. El sqlpackage puede ejecutarse en macOS y Linux.

| Problema conocido | Detalles |
| :---------- | :------ |
| Los colaboradores de compilación y de implementación no se admiten. | &nbsp; |
| No se admiten archivos .dacpac y .bacpac antiguos que utilizan la serialización de datos de json. | &nbsp; |
| Es posible que los archivos .dacpac a los que se hace referencia (por ejemplo, master.dacpac) no se resuelvan debido a problemas con sistemas de archivos que distinguen entre mayúsculas y minúsculas. | Una solución consiste en poner en mayúscula el nombre del archivo de referencia (por ejemplo MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

Fecha de publicación: &nbsp; 24 de octubre de 2018  
Compilación: &nbsp; 15.0.4200.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó compatibilidad para el nivel de compatibilidad de la base de datos 150. | &nbsp; |
| Se agregó compatibilidad para instancias administradas. | &nbsp; |
| Se agregó el parámetro de línea de comandos MaxParallelism para especificar el grado de paralelismo para las operaciones de base de datos. | &nbsp; |
| Se agregó el parámetro de línea de comandos AccessToken para especificar un token de autenticación al conectarse a SQL Server. | &nbsp; |
| Se agregó compatibilidad para tipos de datos BLOB y CLOB en secuencia para las importaciones. | &nbsp; |
| Se agregó compatibilidad con la opción escalar "INLINE" de UDF. | &nbsp; |
| Se agregó compatibilidad con la sintaxis "MERGE" de la tabla de grafos. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Se corrigió la pseudocolumna no resuelta para las tablas de grafos. | &nbsp; |
| Se corrigió la creación de una base de datos con grupos de archivos optimizados de memoria cuando se usan tablas optimizadas de memoria. | &nbsp; |
| Se corrigió la inclusión de propiedades extendidas en tablas externas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

Fecha de publicación: &nbsp; 22 de junio de 2018  
Compilación: &nbsp; 14.0.4079.2

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se mejoraron los mensajes de error para errores de conexión, incluido el mensaje de excepción SqlClient. | &nbsp; |
| Compatibilidad con compresión de índices en índices de partición única para importación/exportación. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Se corrigió un problema de ingeniería inversa para conjuntos de columnas XML con SQL 2017 y versiones posteriores. | &nbsp; |
| Se corrigió un problema donde se omitió el scripting en el nivel de compatibilidad de base de datos 140 para Azure SQL Database. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

Fecha de publicación: &nbsp; 25 de enero de 2018  
Compilación: &nbsp; 14.0.3917.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó el parámetro de línea de comandos ThreadMaxStackSize para analizar Transact-SQL con una gran cantidad de instrucciones anidadas. | &nbsp; |
| Compatibilidad con intercalación del catálogo de base de datos. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| Al importar un archivo .bacpac de Azure SQL Database en una instancia local, se corrigieron los errores debidos a que las _claves maestras de base de datos sin la contraseña no se admiten en esta versión de SQL Server_. | &nbsp; |
| Se corrigió el error de pseudocolumna no resuelta para las tablas de grafos. | &nbsp; |
| Se corrigió el uso de SchemaCompareDataModel con autenticación SQL para comparar esquemas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

Fecha de publicación: &nbsp; 12 de diciembre de 2017  
Compilación: &nbsp; 14.0.3881.1

### <a name="features"></a>Características

| Característica | Detalles |
| :------ | :------ |
| Se agregó soporte para la _directiva de retención temporal_ en SQL 2017+ y Azure SQL Database. | &nbsp; |
| Se agregó el parámetro de línea de comandos /DiagnosticsFile:"C:\Temp\sqlpackage.log "para especificar una ruta de archivo para guardar la información de diagnóstico. | &nbsp; |
| Se agregó el parámetro de línea de comandos /Diagnostics para registrar información de diagnóstico en la consola. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>Correcciones

| Fix | Detalles |
| :-- | :------ |
| No bloquear cuando se encuentre un nivel de compatibilidad de base de datos que no entienda. | En su lugar, se asumirá la versión más reciente de Azure SQL Database o la plataforma local. |
| &nbsp; | &nbsp; |
