---
title: WideWorldImportersDW - flujo de trabajo ETL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f33d36cccbbea6f37139410f9d3d6e03f740ee96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067623"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flujo de trabajo de ETL WideWorldImportersDW
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Use la *WWI_Integration* paquete ETL para migrar datos desde la base de datos WideWorldImporters a la base de datos WideWorldImportersDW como cambios de datos. El paquete se ejecute periódicamente (normalmente diariamente).

El paquete garantiza un rendimiento alto mediante el uso de SQL Server Integration Services para coordinar las operaciones masivas T-SQL (en lugar de transformaciones de Integration Services).

Las dimensiones se cargan en primer lugar y, a continuación, se cargan las tablas de hechos. Puede volver a ejecutar el paquete de cualquier momento después de un error.

El flujo de trabajo tiene este aspecto:

 ![Flujo de trabajo de WideWorldImporters ETL](media/wide-world-importers/wideworldimporters-etl-workflow.png)

El flujo de trabajo se inicia con una tarea de expresión que determina el momento adecuado de límite. La hora límite es la hora actual menos unos minutos. (Este enfoque es más sólido que solicita datos directamente a la hora actual). Se truncan los milisegundos desde el momento.

Se inicia el procesamiento principal rellenando la tabla de dimensiones de fecha. El procesamiento garantiza que se han rellenado todas las fechas del año actual en la tabla.

A continuación, en una serie de tareas de flujo de datos se carga cada dimensión. A continuación, se carga cada hecho.

## <a name="prerequisites"></a>Requisitos previos

- SQL Server 2016 (o posterior), con las bases de datos WideWorldImporters y WideWorldImportersDW (en el mismo o en distintas instancias de SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Asegúrese de crear un catálogo de Integration Services. Para crear un catálogo de Integration Services, en el Explorador de objetos de SQL Server Management Studio, haga clic en **Integration Services**y, a continuación, seleccione **Agregar catálogo**. Deje las opciones predeterminadas. Se le solicite para habilitar SQLCLR y proporcione una contraseña.


## <a name="download"></a>Descargar

Para obtener la versión más reciente de la muestra, consulte [wide world importers versión](https://go.microsoft.com/fwlink/?LinkID=800630). Descargue el *ETL.ispac diario* archivo de paquete de Integration Services.

El código fuente volver a crear la base de datos de ejemplo, vea [importadores de todo el mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl).

## <a name="install"></a>Install

1. Implementar el paquete de Integration Services:
   1. En el Explorador de Windows, abra el *ETL.ispac diario* paquete. Esto inicia al Asistente para la implementación de SQL Server Integration Services.
   2. En **Seleccionar origen**, siga los valores predeterminados para la implementación del proyecto, con la ruta de acceso que apunta a la *ETL.ispac diario* paquete.
   3. En **Seleccionar destino**, escriba el nombre del servidor que hospeda el catálogo de Integration Services.
   4. Seleccione una ruta de acceso en el catálogo de Integration Services, por ejemplo, en una carpeta nueva denominada *WideWorldImporters*.
   5. Seleccione **implementar** para finalizar el asistente.

2. Crear un trabajo del Agente SQL Server para el proceso ETL:
   1. En Management Studio, haga clic en **del Agente SQL Server**y, a continuación, seleccione **New** > **trabajo**.
   2. Escriba un nombre, por ejemplo, *WideWorldImporters ETL*.
   3. Agregar un **paso de trabajo** del tipo **paquete SQL Server Integration Services**.
   4. Seleccione el servidor que tiene el catálogo de Integration Services y, a continuación, seleccione el *ETL diario* paquete.
   5. En **configuración** > **administradores de conexión**, asegúrese de que las conexiones de origen y destino están configuradas correctamente. El valor predeterminado es conectarse a la instancia local.
   6. Seleccione **Aceptar** para crear el trabajo.

3. Ejecutar o programar el trabajo.
