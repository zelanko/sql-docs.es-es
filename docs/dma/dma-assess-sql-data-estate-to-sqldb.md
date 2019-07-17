---
title: Evaluar la preparación de un espacio de datos de SQL Server migrar a Azure SQL Database | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar un espacio de datos de SQL Server para la migración a Azure SQL Database
ms.custom: ''
ms.date: 07/16/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: d317fb3f0c2227744318eeaead71514095afbdec
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68269387"
---
# <a name="assess-the-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database-using-the-data-migration-assistant"></a>Evaluar la preparación de un espacio de datos de SQL Server migrar a Azure SQL Database mediante Data Migration Assistant

Migrar cientos de instancias de SQL Server y miles de bases de datos a Azure SQL Database, nuestra oferta de plataforma como servicio (PaaS), son una tarea considerable. Para simplificar el proceso tanto como sea posible, deberá le inspira su preparación relativa para la migración. Identificar la fruta que cuelga de baja, incluidos los servidores y bases de datos que estén totalmente preparados o que requieren un mínimo esfuerzo para preparar la migración, facilita y acelera sus esfuerzos.

En este artículo proporciona instrucciones paso a paso para aprovechar la [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) para resumir los resultados de la preparación y mostrarlos en el [Azure Migrate](https://portal.azure.com/?feature.customPortal=false#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview) concentrador.

## <a name="create-a-project-and-add-a-tool"></a>Cree un proyecto y agregar una herramienta

Configurar un nuevo proyecto de Azure Migrate en una suscripción de Azure y, a continuación, agregar una herramienta.

Un proyecto de Azure Migrate se usa para almacenar la detección, evaluación y recopilados en el entorno está evaluando o migración de metadatos de migración. También usar un proyecto para realizar un seguimiento de los recursos detectados y orquestar la migración y la evaluación.

1. Inicie sesión en Azure portal, seleccione **todos los servicios**y, a continuación, busque Azure Migrate.
2. En **servicios**, seleccione **Azure Migrate**.

   ![Azure Migrate - seleccione servicio](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-services.png)

3. En el **Introducción** página, seleccione **evaluar y migrar bases de datos**.

   ![Azure Migrate - iniciar evaluación](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

4. En **bases de datos**, en **Introducción**, seleccione **agregar cualquier otra herramienta**.

   ![Azure Migrate - agregar herramientas](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tools.png)

5. En el **proyecto migrar** pestaña, seleccione el grupo de recursos y suscripciones de Azure (si aún no tiene un recurso de grupo, cree uno).
6. En **Project Details**, especifique el nombre del proyecto y la ubicación geográfica en la que desea crear el proyecto.

    ![Azure Migrate - agregar un cuadro de diálogo Herramienta](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-add-tool-dialog.png)

    Puede crear un proyecto de Azure Migrate en cualquiera de estas ubicaciones geográficas.

    | **Geography**  | **Región de la ubicación de almacenamiento** |
    | ------------- | ------------- |
    | Asia | Sudeste de Asia o Asia oriental |
    | Europa | Sur de Europa o Europa occidental |
    | Reino Unido | Sur de Reino Unido u oeste de Reino Unido |
    | Estados Unidos | EE. UU. u oeste de EE.UU. 2 |

    La ubicación geográfica especificada para el proyecto solo se usa para almacenar los metadatos recopilados de máquinas virtuales locales. Puede seleccionar cualquier región de destino para la migración real.

7. Seleccione **siguiente**y, a continuación, agregar una herramienta de evaluación.

   > [!NOTE]
   > Cuando crea un proyecto, debe agregar al menos una herramienta de evaluación o la migración.

8. En el **herramienta de evaluación seleccione** ficha, **Azure Migrate: Evaluación de la base de datos** aparece como la herramienta de evaluación para agregar. Si actualmente no tiene una herramienta de evaluación, seleccione el **omitir y agregar una herramienta de evaluación por ahora** casilla de verificación. Seleccione **Next** (Siguiente).

    ![Azure Migrate - pestaña de la herramienta de evaluación de Select](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-assessment-tool.png)

9. En el **herramienta de migración seleccione** ficha, **Azure Migrate: Migración de base de datos** aparece como la herramienta de migración para agregar. Si actualmente no tiene una herramienta de migración, seleccione el **omitir y agregar una herramienta de migración por ahora**. Seleccione **Next** (Siguiente).

    ![Azure Migrate - ficha de la herramienta de migración de Select](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-select-migration-tool.png)

10. En **revisar + agregar herramientas**, revise la configuración y seleccione **agregar herramientas**.

    ![Azure Migrate - revisión + Agregar pestaña herramientas](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-tools.png)

    Después de crear el proyecto, puede seleccionar herramientas adicionales para la evaluación y migración de servidores y cargas de trabajo, las bases de datos y aplicaciones web.

## <a name="assess-and-upload-assessment-results"></a>Evaluar y cargar los resultados de evaluación

Una vez creado correctamente un proyecto de migración, en **herramientas de evaluación**, en el **Azure Migrate: Evaluación de la base de datos** cuadro, instrucciones para descargar y usar la visualización de la herramienta Data Migration Assistant.

   ![Azure Migrate - herramienta de evaluación de agregado](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessment-tool-added.png)

1. Descargar Data Migration Assistant mediante el vínculo proporcionado y, a continuación, instálelo en un equipo con acceso a las instancias de SQL Server de origen.
2. Iniciar el Asistente para migración de datos.

### <a name="create-an-assessment"></a>Crear una evaluación

1. En el lado izquierdo, seleccione el **+** icono y, a continuación, seleccione la evaluación **tipo de proyecto**
2. Especifique el nombre del proyecto y, a continuación, seleccione el servidor de origen y los tipos de servidor de destino.

    Si va a actualizar la instancia de SQL Server local a una versión posterior de SQL Server o SQL Server hospedado en una máquina virtual de Azure, establezca el tipo de servidor de origen y destino **SQL Server**. Establezca el tipo de servidor de destino en **Azure SQL Database Managed Instance** para una evaluación de preparación del destino de Azure SQL Database (PaaS).

3. Seleccione **Crear**.

   ![Azure Migrate - interfaz Data Migration Assistant](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-interface.png)

### <a name="choose-assessment-options"></a>Elegir opciones de evaluación

1. Seleccione el tipo de informe.

    Puede elegir uno o ambos de los siguientes tipos de informes:
    * Comprobar la compatibilidad de base de datos
    * Comprobar paridad de características

   ![Pantalla de opciones de evaluación de Azure Migrate - Data Migration Assistant-](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-options-screen.png)

2. Seleccione **Next** (Siguiente).

### <a name="add-databases-to-assess"></a>Agregar bases de datos para evaluar

1. Seleccione **agregar orígenes** para abrir la marcha conexión menú.
2. Escriba el nombre de instancia SQL server, elija el tipo de autenticación, establezca las propiedades de conexión correcta y, a continuación, seleccione **Connect**.
3. Seleccione las bases de datos para evaluar y, a continuación, seleccione **agregar**.

   > [!NOTE]
   > Puede quitar varias bases de datos seleccionando mientras mantiene presionada la tecla MAYÚS o Ctrl y, a continuación, haga clic en quitar orígenes. También puede agregar las bases de datos de varias instancias de SQL Server con el botón Agregar orígenes.

4. Seleccione **siguiente** para iniciar la evaluación.

   ![Pantalla de Azure Migrate - Data Migration Assistant - seleccione orígenes](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-select-sources-screen.png)

5. Una vez finalizada la evaluación, seleccione **cargar en Azure Migrate**.

   ![Azure Migrate - Data Migration Assistant - revisar resultados de la pantalla](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-dma-review-results-screen.png)

6. Inicie sesión en Azure Portal.

   ![Azure Migrate - Data Migration Assistant - revisar resultados de la pantalla](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-signin.png)

7. Seleccione la suscripción y el proyecto de Azure Migrate en la que desea cargar los resultados de evaluación y, a continuación, seleccione **cargar**.

   Espere la confirmación de la carga de evaluación.

## <a name="view-target-readiness-assessment-results"></a>Ver resultados de la evaluación de preparación de destino

1. Inicie sesión en Azure portal, busque Azure migrate y seleccione **Azure Migrate**.

   ![Búsqueda del servicio de Azure Migrate - Azure portal:](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-portal-search.png)

2. Seleccione **evaluar y migrar bases de datos** para llegar a los resultados de evaluación.

   ![Azure Migrate - revisar resultados de evaluación](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-hub-assess.png)

    Puede ver el resumen de preparación de SQL Server, asegúrese de que se encuentra en el proyecto de migración más adecuado, en caso contrario, use cambiar la opción de seleccionar un proyecto de migración diferentes.

    Migrar el proyecto cada vez que actualice los resultados de evaluación en Azure, Azure migrate concentrador consolidar todos los resultados y proporcionar el informe de resumen.  Puede ejecutar varias evaluaciones Data Migration Assistant en paralelo y cargar los resultados en el proyecto de migración solo para obtener el informe de preparación consolidada.

   ![Azure Migrate - resultados de preparación para la revisión](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-review-readiness.png)

    **Evalúa las instancias de base de datos**:  El número de instancias de SQL Server evaluado hasta ahora.
    **Evalúa las bases de datos**: Número total de bases de datos que se evalúa a través de una o varias instancias de SQL Server evaluadas **bases de datos está listo para la base de datos SQL**:  Número de bases de datos está listos para migrar a Azure SQL Database (PaaS).
    **Las bases de datos está listo para la máquina virtual de SQL Azure**:  Número de bases de datos constan uno o varios bloqueadores de migración a Azure SQL Database (PaaS), pero se pueden migrar a las máquinas virtuales de Azure SQL Server.

3. Seleccione **evalúa las instancias de base de datos** para llegar a la vista de nivel de instancia de SQL Server.

   ![Azure Migrate - preparación de la instancia de revisión](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-instances.png)

    Puede encontrar el estado de preparación de porcentaje de cada instancia de SQL Server, migrar a Azure SQL Database (PaaS).

4. Seleccione una instancia específica para llegar a la vista de preparación de la base de datos.

   ![Azure Migrate - preparación de la base de datos de revisión](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-assessed-databases.png)

    Puede ver el número de bloqueadores de migración por cada base de datos, el destino recomendado por cada base de datos en la vista anterior.

5. Revise los resultados de evaluación de DMA para obtener más detalles en torno a los bloqueadores de migración.

   ![Azure Migrate - bloqueadores de migración de revisión](../dma/media//dma-assess-sql-data-estate-to-sqldb/dms-azure-migrate-migration-blockers.png)

## <a name="see-also"></a>Vea también

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
* [Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)
