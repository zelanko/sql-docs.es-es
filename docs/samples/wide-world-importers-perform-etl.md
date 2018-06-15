---
title: 'WideWorldImportersDW: flujo de trabajo ETL | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36638c4cc2bda58ac277822d5c4a4ce5421ab8b4
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467691"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flujo de trabajo de WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use la *WWI_Integration* paquete ETL para migrar datos desde la base de datos WideWorldImporters a la base de datos de WideWorldImportersDW cuando los datos cambian. El paquete se ejecuta periódicamente (normalmente diariamente).

El paquete garantiza un rendimiento alto mediante el uso de SQL Server Integration Services para realizar operaciones masivas T-SQL (en lugar de transformaciones independientes en Integration Services).

Dimensiones se cargan en primer lugar y, a continuación, se cargan las tablas de hechos. Puede volver a ejecutar el paquete cualquier momento después de un error.

El flujo de trabajo tiene el siguiente aspecto:

 ![Flujo de trabajo de WideWorldImporters ETL](media/wide-world-importers/wideworldimporters-etl-workflow.png)

El flujo de trabajo se inicia con una tarea de expresión que determina el límite de tiempo adecuado. El tiempo límite es la hora actual menos unos minutos. (Este enfoque es más estable que solicita datos directamente a la hora actual). Se truncan los milisegundos desde el momento.

Inicia el procesamiento principal ya que rellena la tabla de dimensiones de fecha. El procesamiento se asegura de que se han rellenado todas las fechas del año actual en la tabla.

A continuación, en una serie de tareas de flujo de datos se carga cada dimensión. A continuación, se carga cada hecho.

## <a name="prerequisites"></a>Requisitos previos

- SQL Server 2016 (o posterior), con las bases de datos WideWorldImporters y WideWorldImportersDW (en el mismo o en distintas instancias de SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Asegúrese de que crea un catálogo de Integration Services. Para crear un catálogo de Integration Services, en el Explorador de objetos de SQL Server Management Studio, haga clic en **Integration Services**y, a continuación, seleccione **Add Catalog**. Deje las opciones predeterminadas. Deberá habilitar SQLCLR y proporcione una contraseña.


## <a name="download"></a>Descargar

Para obtener la versión más reciente de la muestra, vea [wide world importers versión](http://go.microsoft.com/fwlink/?LinkID=800630). Descargue el *ETL.ispac diaria* archivo de paquete de Integration Services.

Para que el código fuente volver a crear la base de datos de ejemplo, vea [importadores de todo el mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl).

## <a name="install"></a>Install

1. Implementar el paquete de Integration Services:
   1. En el Explorador de Windows, abra la *ETL.ispac diaria* paquete. Esto inicia al Asistente para la implementación de SQL Server Integration Services.
   2. En **Seleccionar origen**, siga los valores predeterminados para la implementación del proyecto, con la ruta de acceso que señala a la *ETL.ispac diaria* paquete.
   3. En **Seleccionar destino**, escriba el nombre del servidor que hospeda el catálogo de Integration Services.
   4. Seleccione una ruta de acceso en el catálogo de Integration Services, por ejemplo, en una carpeta nueva denominada *WideWorldImporters*.
   5. Seleccione **implementar** para finalizar el asistente.

2. Crear un trabajo de agente SQL Server para el proceso ETL:
   1. En Management Studio, haga clic en **Agente SQL Server**y, a continuación, seleccione **New** > **trabajo**.
   2. Escriba un nombre, por ejemplo, *WideWorldImporters ETL*.
   3. Agregar un **paso de trabajo** del tipo **paquete SQL Server Integration Services**.
   4. Seleccione el servidor que tiene el catálogo de Integration Services y, a continuación, seleccione la *ETL diaria* paquete.
   5. En **configuración** > **administradores de conexión**, asegúrese de que las conexiones de origen y de destino están configuradas correctamente. El valor predeterminado es para conectarse a la instancia local.
   6. Seleccione **Aceptar** para crear el trabajo.

3. Ejecutar o programar el trabajo.
