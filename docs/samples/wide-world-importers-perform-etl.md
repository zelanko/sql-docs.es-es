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
robots: noindex,nofollow
ms.openlocfilehash: c5a9508d19d1a9028ab5d9f1b78caf6988acb925
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-etl-workflow"></a>Flujo de trabajo de WideWorldImportersDW ETL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
El paquete ETL WWI_Integration se usa para migrar datos de la base de datos WideWorldImporters a la base de datos WideWorldImportersDW como los cambios de datos. El paquete se ejecuta periódicamente (normalmente cada día).

## <a name="overview"></a>Información general

El diseño de los usos de paquete SQL Server Integration Services (SSIS) para realizar operaciones masivas T-SQL (en lugar de como transformaciones independientes dentro de SSIS) para asegurar un rendimiento alto.

Dimensiones se cargan en primer lugar, seguida de las tablas de hechos. Puede volver a ejecutar el paquete en cualquier momento después de un error.

El flujo de trabajo es como sigue:

 ![Flujo de trabajo de WideWorldImporters ETL](media/wide-world-importers/wideworldimporters-etl-workflow.png)

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
