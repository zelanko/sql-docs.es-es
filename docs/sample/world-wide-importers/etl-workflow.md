---
title: Flujo de trabajo ETL | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 06/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 679e58fe-b062-4934-a94c-9bb916b0bcb0
caps.latest.revision: "5"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: bbda77b86b4c804ae0cf261f54f51fc487090e1d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flujo de trabajo de WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]El paquete ETL WWI_Integration se usa para migrar datos de la base de datos WideWorldImporters a la base de datos WideWorldImportersDW como los cambios de datos. El paquete se ejecuta periódicamente (normalmente cada día).

## <a name="overview"></a>Información general

El diseño de los usos de paquete SQL Server Integration Services (SSIS) para realizar operaciones masivas T-SQL (en lugar de como transformaciones independientes dentro de SSIS) para asegurar un rendimiento alto.

Dimensiones se cargan en primer lugar, seguida de las tablas de hechos. Puede volver a ejecutar el paquete en cualquier momento después de un error.

El flujo de trabajo es como sigue:

 ![Flujo de trabajo de WideWorldImporters ETL](../../sample/world-wide-importers/media/wideworldimporters-etl-workflow.png)

Se inicia con una tarea de expresión que funciona la hora límite adecuado. Este tiempo es la hora actual menos unos minutos. (Esto es más estable que solicita datos directamente a la hora actual). A continuación, se trunca los milisegundos desde el momento.

Inicia el procesamiento principal ya que rellena la tabla de dimensiones de fecha. Se asegura de que se han rellenado todas las fechas del año actual en la tabla.

Después de esto, una serie de tareas de flujo de datos carga cada dimensión y, a continuación, cada hecho.

## <a name="prerequisites"></a>Requisitos previos

- SQL Server 2016 (o superior) con las bases de datos WideWorldImporters y WideWorldImportersDW. Puede tratarse de la mismas o distintas instancias de SQL Server.
- SQL Server Management Studio (SSMS)
- SQL Server 2016 Integration Services (SSIS).
  - Asegúrese de que haya creado un catálogo de SSIS. Si no es así, haga clic en **Integration Services** en el Explorador de objetos de SSMS y elija **Add Catalog**. Siga los valores predeterminados. Le pedirá que habilite sqlclr y proporcione una contraseña.


## <a name="download"></a>Descargar

La versión más reciente del ejemplo:

[Wide world importers versión](http://go.microsoft.com/fwlink/?LinkID=800630)

Descargue el archivo de paquete SSIS **ETL.ispac diario**.

Código fuente para volver a crear la base de datos de ejemplo está disponible en la ubicación siguiente.

[importadores de todo el mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Install

1. Implementar el paquete SSIS.
   - Abra el paquete de "Diario ETL.ispac" desde el Explorador de Windows. Se iniciará al Asistente para la implementación de Integration Services.
   - En "Seleccionar archivos de origen" siga la implementación del proyecto, de forma predeterminada con la ruta de acceso que apunta al paquete de "Diario ETL.ispac".
   - En "Seleccionar destino", escriba el nombre del servidor que hospeda el catálogo de SSIS.
   - Seleccione una ruta de acceso en el catálogo de SSIS, por ejemplo en una nueva carpeta "WideWorldImporters".
   - Finalice al asistente, haga clic en implementar.

2. Crear un trabajo de agente SQL Server para el proceso ETL.
   - En SSMS, menú contextual "Agente SQL Server" y seleccione Nuevo -> trabajos.
   - Elija un nombre, por ejemplo, "WideWorldImporters ETL".
   - Agregue un paso de trabajo de tipo "Paquete de SQL Server Integration Services".
   - Seleccione el servidor con el catálogo de SSIS y seleccione el paquete de "Diario ETL".
   - En Configuración -> administradores de conexión garantiza las conexiones de origen y de destino estén configuradas correctamente. El valor predeterminado es para conectarse a la instancia local.
   - Haga clic en Aceptar para crear el trabajo.

3. Ejecutar o programar el trabajo.
