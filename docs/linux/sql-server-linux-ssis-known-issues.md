---
title: Limitaciones y problemas conocidos de SSIS en Linux | Documentos de Microsoft
description: "Este artículo describen las limitaciones y problemas conocidos de SQL Server Integration Services (SSIS) en equipos Linux"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 96bf588edd15c77caa6649ac04b6a95046135e95
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitaciones y problemas conocidos de SSIS en Linux

Este tema describe las limitaciones actuales y problemas conocidos de SQL Server Integration Services (SSIS) en Linux.

## <a name="general-limitations-and-known-issues"></a>Tiene las limitaciones y problemas conocidos

Las siguientes características no se admiten en esta versión de SSIS en Linux:
  - Base de datos de catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Ampliación SSIS
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para conocer otras limitaciones y problemas conocidos de SSIS en Linux, consulte la [notas de la versión](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a>Componentes admitidos y no admitidos

Se admiten los siguientes componentes de Integration Services integrados en Linux. Algunos de ellos tienen limitaciones en la plataforma de Linux, tal como se describe en las tablas siguientes.

Componentes integrados que no se muestran aquí no se admiten en Linux.

### <a name="supported-control-flow-tasks"></a>Admite tareas de flujo de control
- Inserción masiva, tarea
- Tarea Flujo de datos
- Tarea de generación de perfiles de datos
- Tarea Ejecutar SQL
- Tarea Ejecutar instrucción T-SQL
- Texto Expresión
- Tarea FTP
- Tarea Servicio web
- Tarea XML

### <a name="control-flow-tasks-supported-with-limitations"></a>Tareas de flujo de control compatibles con limitaciones

| Tarea | Limitaciones |
|------------|---|
| Tarea Ejecutar proceso | Solo es compatible con el modo en proceso. |
| Tarea sistema de archivos | El *mover directorio* y *establecer atributos de archivo* no se admiten las acciones. |
| tarea Script | Solo es compatible con API estándar de .NET Framework. |
| Enviar correo, tarea | Solo admite el modo de usuario anónimo. |
| Tarea de transferencia de base de datos | No se admiten las rutas de acceso UNC. |
| | |

### <a name="supported-control-flow-containers"></a>Admite contenedores de flujo de control
- contenedor de secuencias
- Contenedor de bucles For
- Contenedor Foreach Loop

### <a name="supported-data-flow-sources-and-destinations"></a>Orígenes de flujo de datos admitidos y los destinos
- Destino y origen de archivo sin formato
- Origen XML

### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Orígenes de flujo de datos y destinos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| ADO.NET, origen y destino | Solo se admite el proveedor de datos SQLClient. |
| Destino y origen de archivo plano | Solo se admiten rutas de acceso de archivo de estilo de Windows, al que se aplica la regla de asignación de ruta de acceso predeterminada. Por ejemplo `D:\home\ssis\travel.csv` se convierte en `/home/ssis/travel.csv`. |
| Origen OData | Solo se admite la autenticación básica. |
| Destino y origen de ODBC | Es compatible con controladores de 64 bits Unicode ODBC en Linux. Depende del Administrador de controladores UnixODBC en Linux. |
| Destino y origen de OLE DB | Solo se admiten SQL Server Native Client 11.0 y proveedor Microsoft OLE DB para SQL Server. |
| | |

### <a name="supported-data-flow-transformations"></a>Admite las transformaciones de flujo de datos
- Agregado
- Auditar
- Balanced Data Distributor
- Mapa de caracteres
- División condicional
- Copiar columna
- Conversión de datos
- Columna derivada
- Exportar columna
- agrupación aproximada
- Búsqueda aproximada
- Importar columna
- Lookup
- Mezcla
- Merge Join
- Multidifusión
- Dinamización
- Recuento de filas
- Dimensión de variación lenta
- Sort
- Búsqueda de términos
- Unión de todo
- Anulación de dinamización

### <a name="data-flow-transformations-supported-with-limitations"></a>Transformaciones de flujo de datos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| transformación Comando de OLE DB | Mismas limitaciones que el origen de OLE DB y el destino. |
| componente de script | Solo es compatible con API estándar de .NET Framework. |
| | |

### <a name="supported-and-unsupported-log-providers"></a>Proveedores de registro compatibles y no compatibles
Todos los proveedores de registro SSIS integrados se admiten en Linux excepto el proveedor de registro de eventos de Windows.

El proveedor de registro de SQL Server admite únicamente la autenticación de SQL; no admite la autenticación de Windows.

Los proveedores de registro SSIS para archivos de texto, para los archivos XML y de SQL Server Profiler escriben sus resultados a un archivo que especifique. Las consideraciones siguientes se aplican a la ruta de acceso de archivo:
-   Si no proporciona una ruta de acceso, el proveedor de registro se escribe en el directorio actual del host. Si el usuario actual no tiene permiso para escribir en el directorio actual del host, el proveedor de registro genera un error.
-   No se puede usar una variable de entorno en una ruta de acceso de archivo. Si especifica una variable de entorno, aparece el texto literal que se especifique en la ruta de acceso de archivo. Por ejemplo, si especifica `%TMP%/log.txt`, el proveedor de registro anexa el texto literal `/%TMP%/log.txt` en el directorio actual del host.

