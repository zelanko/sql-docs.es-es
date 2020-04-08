---
title: Realizar una evaluación de migración de SQL Server
titleSuffix: Data Migration Assistant
description: Aprenda a usar Data Migration Assistant para evaluar un SQL Server local antes de migrar a otro SQL Server SQL Server o a Azure SQL Database
ms.date: 01/15/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809751"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Evaluación de la migración de SQL Server con Data Migration Assistant

Las siguientes instrucciones paso a paso le ayudan a realizar su primera evaluación para migrar a SQL Server local, SQL Server que se ejecuta en una máquina virtual de Azure o Azure SQL Database mediante el Asistente para migración de datos.

   > [!NOTE]
   > Data Migration Assistant v5.0 presenta compatibilidad para analizar la conectividad de base de datos y las consultas SQL incrustadas en el código de la aplicación. Para obtener más información, consulte la entrada de blog Uso del Asistente para migración de datos para evaluar la capa de [acceso a datos de una aplicación.](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430)

## <a name="create-an-assessment"></a>Crear una evaluación

1. Seleccione el icono **Nuevo** (+) y, a continuación, seleccione el tipo de proyecto **Evaluación.**

2. Establezca el tipo de servidor de origen y de destino.

    Si va a actualizar la instancia de SQL Server local a una instancia de SQL Server local moderna o a SQL Server hospedada en una máquina virtual de Azure, establezca el tipo de servidor de origen y de destino en **SQL Server**. Si va a migrar a Azure SQL Database, establezca el tipo de servidor de destino **en Azure SQL Database**.

3. Haga clic en **Crear**.

   ![Crear una evaluación](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>Elija las opciones de evaluación

1. Seleccione la versión de SQL Server de destino a la que va a migrar.

2. Seleccione el tipo de informe.

   Al evaluar la instancia de SQL Server de origen para migrar a SQL Server local o a SQL Server hospedado en destinos de máquina virtual de Azure, puede elegir uno o ambos de los siguientes tipos de informe de evaluación:

    - **Problemas de compatibilidad**
    - **Recomendación de las nuevas características**

   ![Seleccione un tipo de informe de evaluación para el destino de SQL Server](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Al evaluar la instancia de SQL Server de origen para migrar a Azure SQL Database, puede elegir uno o ambos de los siguientes tipos de informe de evaluación:

    - **Check database compatibility (Comprobar compatibilidad de bases de datos)**
    - **Check feature parity (Comprobar paridad de características)**

    ![Seleccione el tipo de informe de evaluación para el destino de SQL Database](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>Agregue bases de datos y seguimiento de eventos extendidos para evaluar

1. Seleccione **Agregar orígenes** para abrir el menú desplegable de conexión.

2. Escriba el nombre de la instancia del servidor SQL, elija el tipo de autenticación, establezca las propiedades de conexión correctas y, a continuación, seleccione **Conectar**.

3. Seleccione las bases de datos que desea evaluar y, a continuación, seleccione **Agregar**.

    > [!NOTE]
    > Puede quitar varias bases de datos seleccionándolas mientras mantiene pulsada la tecla Mayús o Ctrl y, a continuación, haga clic en **Quitar orígenes**. También puede agregar bases de datos desde varias instancias de SQL Server seleccionando **Agregar orígenes**.

4. Si tiene consultas SQL ad hoc o dinámicas o cualquier instrucción DML iniciada a través de la capa de datos de la aplicación, escriba la ruta de acceso a la carpeta en la que colocó todos los archivos de sesión de eventos extendidos que recopiló para capturar la carga de trabajo en el SQL Server de origen.

     En el ejemplo siguiente se muestra cómo crear una sesión de eventos extendidos en el SQL Server SQL Server de origen para capturar la carga de trabajo de la capa de datos de la aplicación.  Capture la carga de trabajo durante la duración que representa la carga de trabajo máxima.

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. Haga clic en **Siguiente** para iniciar la evaluación.

    ![Añadir fuentes e iniciar la evaluación](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> Para ejecutar varias evaluaciones simultáneamente y ver su estado, abra la página **All Assessments** (Todas las evaluaciones).

## <a name="view-results"></a>Vista de resultados

La duración de la evaluación depende del número de bases de datos agregadas y del tamaño del esquema de cada base de datos. Los resultados se muestran para cada base de datos tan pronto como están disponibles.

1. Seleccione la base de datos que ha completado la evaluación y, a continuación, cambie entre problemas de **compatibilidad** y **recomendaciones** de características mediante el conmutador.

2. Revise los problemas de compatibilidad en todos los niveles de compatibilidad admitidos por la versión de SQL Server de destino que seleccionó en la página **Opciones.**

Puede revisar los problemas de compatibilidad analizando el objeto afectado, sus detalles y potencialmente una corrección para cada problema identificado en **Cambios**de interrupción , **Cambios**de comportamiento y **Características en desuso**.

![Ver los resultados de la evaluación](../dma/media/dma-assesssqlonprem/review-results.png)

Del mismo modo, puede revisar la recomendación de características en las áreas **Rendimiento,** **Almacenamiento**y **Seguridad.**

Las recomendaciones de características cubren diferentes tipos de características, como OLTP en memoria, almacén de columnas, Stretch Database, Always Encrypted, Dynamic Data Masking y cifrado de datos transparente.

![Ver recomendaciones de características](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Para Azure SQL Database, las evaluaciones proporcionan problemas de bloqueo de migración y problemas de paridad de características.Revise los resultados de ambas categorías seleccionando las opciones específicas.

- La categoría de **paridad** de características de SQL Server proporciona un conjunto completo de recomendaciones, enfoques alternativos disponibles en Azure y pasos de mitigación. Le ayuda a planificar este esfuerzo en sus proyectos de migración.

  ![Ver información para la paridad de características de SQL Server](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- La categoría Problemas de **compatibilidad** proporciona características parcialmente admitidas o no admitidas que bloquean la migración de bases de datos de SQL Server locales a bases de datos SQL de Azure.A continuación, proporciona recomendaciones para ayudarle a abordar esos problemas.

  ![Ver problemas de compatibilidad](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>Evaluar un estado de datos para la preparación del objetivo

Si desea ampliar aún más estas evaluaciones a todo el estado de datos y encontrar la preparación relativa de las instancias de SQL ServerySQL Server y las bases de datos para la migración a Azure SQL Database, cargue los resultados en el centro de Azure Migrate seleccionando **Upload to Azure Migrate**.

Si lo hace, podrá ver los resultados consolidados en el proyecto de concentrador Azure Migrate.

Aquí encontrará instrucciones detalladas paso a paso para las evaluaciones de preparación de [objetivos.](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)

   ![Cargar resultados en Azure Migrate](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>Exportar resultados

Una vez que todas las bases de datos finalicen la evaluación, seleccione **Exportar informe** para exportar los resultados a un archivo JSON o csv. A continuación, puede analizar los datos a su conveniencia.

## <a name="save-and-load-assessments"></a>Guardado y carga de evaluaciones

Además de exportar los resultados de una evaluación, puede guardar los detalles de la evaluación en un archivo y cargar un archivo de evaluación para su revisión posterior.  Para obtener más información, consulte el artículo [Guardar y cargar evaluaciones con Data Migration Assistant](../dma/dma-save-load-assessments.md).
