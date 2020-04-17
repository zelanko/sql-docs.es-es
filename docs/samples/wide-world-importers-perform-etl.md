---
title: WideWorldImportersDW - Flujo de trabajo de ETL Microsoft Docs
description: Use el paquete ETL con SQL Server Integration Services (SSIS) para migrar periódicamente datos de la base de datos WideWorldImporters a WideWorldImportersDW.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487434"
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flujo de trabajo De WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Utilice el paquete ETL *WWI_Integration* para migrar datos de la base de datos WideWorldImporters a la base de datos WideWorldImportersDW a medida que cambian los datos. El paquete se ejecuta periódicamente (generalmente todos los días).

El paquete garantiza un alto rendimiento mediante SQL Server Integration ServicesIntegration Services para organizar las operaciones masivas de T-SQL (en lugar de transformaciones independientes en Integration ServicesIntegration Services).

Las dimensiones se cargan primero y, a continuación, se cargan las tablas de hechos. Puede volver a ejecutar el paquete en cualquier momento después de un error.

El flujo de trabajo tiene este aspecto:

 ![Flujo de trabajo De WideWorldImporters ETL](media/wide-world-importers/wideworldimporters-etl-workflow.png)

El flujo de trabajo comienza con una tarea de expresión que determina el tiempo de corte adecuado. El tiempo límite es el tiempo actual menos unos minutos. (Este enfoque es más robusto que solicitar datos directamente a la hora actual.) Los milisegundos se truncan a partir del momento.

El procesamiento principal comienza rellenando la tabla de dimensiones Date. El procesamiento garantiza que todas las fechas del año actual se hayan rellenado en la tabla.

A continuación, una serie de tareas de flujo de datos carga cada dimensión. Luego, cargan cada hecho.

## <a name="prerequisites"></a>Prerrequisitos

- SQL Server 2016 (o posterior), con las bases de datos WideWorldImporters y WideWorldImportersDW (en la misma instancia o en diferentes instancias de SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Asegúrese de crear un catálogo de Integration ServicesIntegration Services . Para crear un catálogo de Integration ServicesIntegration Services , en el Explorador de objetos de SQL Server Management StudioSQL Server Management Studio , haga clic con el botón secundario en **Integration ServicesIntegration Services**y, a continuación, seleccione **Agregar catálogo**. Deje las opciones predeterminadas. Se le pedirá que habilite SQLCLR y proporcione una contraseña.


## <a name="download"></a>Descargar

Para obtener la última versión de la muestra, véase [wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630). Descargue el archivo de paquete *De ETL.ispac* Integration Services daily.

Para que el código fuente vuelva a crear la base de datos de ejemplo, vea [wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis).

## <a name="install"></a>Instalar

1. Implemente el paquete de Integration ServicesIntegration Services:
   1. En el Explorador de Windows, abra el paquete *Daily ETL.ispac.* Esto inicia el Asistente para la implementación de SQL Server Integration ServicesIntegration Services .
   2. En **Seleccionar origen**, siga los valores predeterminados para la implementación de proyectos, con la ruta de acceso que apunta al paquete Diario *ETL.ispac.*
   3. En **Seleccionar destino**, escriba el nombre del servidor que hospeda el catálogo de Integration ServicesIntegration Services .
   4. Seleccione una ruta de acceso en el catálogo de Integration ServicesIntegration Services , por ejemplo, en una nueva carpeta denominada *WideWorldImporters*.
   5. Seleccione **Implementar** para finalizar el asistente.

2. Cree un trabajo del Agente SQL ServerPARAel para el proceso ETL:
   1. En Management StudioManagement Studio , haga clic con el botón secundario en **Agente SQL Server**y, a continuación, seleccione **Nuevo** > **trabajo**.
   2. Escriba un nombre, por ejemplo, *WideWorldImporters ETL*.
   3. Agregue un **paso** de trabajo del tipo Paquete de **SQL Server Integration Services**.
   4. Seleccione el servidor que tiene el catálogo de Integration ServicesIntegration Services y, a continuación, seleccione el paquete *ETL diario.*
   5. En **Configuration** > **Connection Managers**, asegúrese de que las conexiones al origen y al destino están configuradas correctamente. El valor predeterminado es conectarse a la instancia local.
   6. Seleccione **Aceptar** para crear el trabajo.

3. Ejecute o programe el trabajo.
