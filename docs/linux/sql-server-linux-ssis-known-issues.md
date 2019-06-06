---
title: Limitaciones y problemas conocidos de SSIS en Linux | Microsoft Docs
description: En este artículo se describe problemas conocidos y limitaciones para SQL Server Integration Services (SSIS) en equipos Linux
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: fdf6542f64549233dd5d4ef15dc39a53fefa49a3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712836"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Limitaciones y problemas conocidos de SSIS en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe problemas conocidos y limitaciones para SQL Server Integration Services (SSIS) en Linux.

## <a name="general-limitations-and-known-issues"></a>Problemas conocidos y limitaciones generales

Las siguientes características no se admiten en esta versión de SSIS en Linux:
  - Base de datos del catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Escalabilidad horizontal de SSIS
  - Azure Feature Pack para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para otras limitaciones y problemas conocidos de SSIS en Linux, consulte el [notas de la versión](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a> Componentes admitidos y no admitidos

Se admiten los siguientes componentes de Integration Services integrados en Linux. Algunos de ellos tienen limitaciones en la plataforma Linux. Los componentes integrados que no se muestran aquí no se admiten en Linux.

## <a name="supported-control-flow-tasks"></a>Admite tareas de flujo de control
- Inserción masiva, tarea
- tarea Flujo de datos
- Tarea de generación de perfiles de datos
- Tarea Ejecutar SQL
- Tarea Ejecutar instrucción T-SQL
- Texto Expresión
- Tarea FTP
- Tarea Servicio web
- Tarea XML

## <a name="control-flow-tasks-supported-with-limitations"></a>Tareas de flujo de control compatibles con limitaciones

| Tarea | Limitaciones |
|------------|---|
| Tarea Ejecutar proceso | Solo se admite el modo en proceso. |
| Tarea sistema de archivos | El *mover directorio* y *establecer atributos de archivo* no se admiten las acciones. |
| tarea Script | Solo es compatible con las API de .NET Framework estándar. |
| Enviar correo, tarea | Solo admite el modo de usuario anónimo. |
| Tarea de transferencia de base de datos | No se admiten las rutas de acceso UNC. |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>Tareas del plan de mantenimiento compatibles y no compatibles

En un plan de mantenimiento de SQL Server, normalmente puede utilizar una variedad de tareas SSIS.

No se admiten las siguientes tareas del plan de mantenimiento en Linux:
- Notificar al operador
- Ejecutar trabajo del Agente SQL Server

Se admiten las siguientes tareas del plan de mantenimiento en Linux:
- Comprobar la integridad de la base de datos
- Reducir base de datos
- Reorganizar índice
- Volver a generar índice
- Actualizar estadísticas
- Limpiar historial
- Realizar copias de seguridad de base de datos
- Instrucción de Transact-SQL

## <a name="supported-control-flow-containers"></a>Admite contenedores de flujo de control
- contenedor de secuencias
- Contenedor de bucles For
- Contenedor Foreach Loop

## <a name="supported-data-flow-sources-and-destinations"></a>Orígenes de flujo de datos admitidos y los destinos
- Destino y origen de archivo sin formato
- Origen XML

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Orígenes de flujo de datos y destinos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| Destino y origen de ADO.NET | Solo se admite el proveedor de datos SQLClient. |
| Destino y origen de archivo plano | Solo se admiten rutas de acceso de archivo de estilo de Windows, al que se aplica la regla de asignación de ruta de acceso predeterminada. Por ejemplo `D:\home\ssis\travel.csv` se convierte en `/home/ssis/travel.csv`. |
| Origen OData | Solo admite la autenticación básica. |
| Origen y destino de ODBC | Es compatible con controladores de 64 bits Unicode ODBC en Linux. Depende del Administrador de controladores UnixODBC en Linux. |
| Destino y origen de OLE DB | Solo se admiten SQL Server Native Client 11.0 y el proveedor Microsoft OLE DB para SQL Server. |
| | |

## <a name="supported-data-flow-transformations"></a>Admite las transformaciones de flujo de datos
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

## <a name="data-flow-transformations-supported-with-limitations"></a>Transformaciones de flujo de datos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| transformación Comando de OLE DB | Mismas limitaciones que el origen de OLE DB y el destino. |
| componente de script | Solo es compatible con las API de .NET Framework estándar. |
| | |

## <a name="supported-and-unsupported-log-providers"></a>Proveedores de registro compatibles y no compatibles
Todos los proveedores de registro integrados de SSIS se admiten en Linux excepción el proveedor de registro de eventos de Windows.

El proveedor de registro de SQL Server admite únicamente la autenticación de SQL; no se admite la autenticación de Windows.

Los proveedores de registro SSIS para archivos de texto, para archivos XML y para SQL Server Profiler escriben sus resultados a un archivo que especifique. Las siguientes consideraciones se aplican a la ruta de acceso de archivo:
-   Si no proporciona una ruta de acceso, el proveedor de registro se escribe en el directorio actual del host. Si el usuario actual no tiene permiso para escribir en el directorio actual del host, el proveedor de registro genera un error.
-   No se puede usar una variable de entorno en una ruta de acceso de archivo. Si especifica una variable de entorno, aparece el texto literal que se especifica en la ruta de acceso de archivo. Por ejemplo, si especifica `%TMP%/log.txt`, el proveedor de registro anexa el texto literal `/%TMP%/log.txt` en el directorio actual del host.

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Ejecución en Linux con cron de paquetes de programación de SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
