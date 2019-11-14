---
title: Migre SQL Server a Azure SQL Database mediante el Data Migration Assistant
description: Aprenda a usar Data Migration Assistant para migrar un SQL Server local a Azure SQL Database
ms.date: 07/15/2019
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
ms.custom: seo-lt-2019
ms.openlocfilehash: cc87b541b2b6ebf2f6a9068ba35ae0f62f8e9988
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056612"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Migre SQL Server o SQL Server locales en máquinas virtuales de Azure para Azure SQL Database con el Data Migration Assistant

El Data Migration Assistant proporciona evaluaciones sin problemas de SQL Server locales y actualizaciones a versiones posteriores de SQL Server o migraciones a SQL Server en máquinas virtuales de Azure o Azure SQL Database.

En este artículo se proporcionan instrucciones paso a paso para migrar SQL Server de forma local a Azure SQL Database mediante el Data Migration Assistant.

## <a name="create-a-new-migration-project"></a>Crear un nuevo proyecto de migración

1. En el panel izquierdo, seleccione **nuevo** (+) y, a continuación, seleccione el tipo de proyecto de **migración** .

2. Establezca el tipo de origen en **SQL Server** y el tipo de servidor de destino en **Azure SQL Database**.

3. Seleccione **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>Especificar el servidor de origen y la base de datos

1. En el origen, en **conectar con el servidor de origen**, en el cuadro de texto **nombre de servidor** , escriba el nombre de la instancia de SQL Server de origen.

2. Seleccione el **tipo de autenticación** admitido por la instancia de SQL Server de origen.

   > [!NOTE]
   > Se recomienda cifrar la conexión activando la casilla **cifrar conexión** en **conexión poperties**.

    ![Seleccionar servidor de origen](../dma/media/select-source-server.png)

3. Seleccione **Conectar**.

4. Seleccione una única base de datos de origen para migrar a Azure SQL Database.

   > [!NOTE]
   > Si desea evaluar la base de datos y ver y aplicar las correcciones recomendadas antes de la migración, active la casilla **evaluar la base de datos antes** de la migración.

    ![Seleccionar base de datos de origen](../dma/media/select-source-database.png)

5. Seleccione **Siguiente**.

## <a name="specify-the-target-server-and-database"></a>Especificar el servidor de destino y la base de datos

1. En el destino, en el cuadro de texto **nombre del servidor** , en **conectar con el servidor de destino**, escriba el nombre de la instancia de Azure SQL Database. 

2. Seleccione el **tipo de autenticación** admitido por la instancia de Azure SQL Database de destino.

   > [!NOTE]
   > Se recomienda cifrar la conexión activando la casilla **cifrar conexión** en **conexión poperties**.

     ![Seleccionar servidor de destino](../dma/media/select-target-server.png)

3. Seleccione **Conectar**.

4. Seleccione una única base de datos de destino a la que migrar.

   > [!NOTE]
   > Si tiene previsto migrar usuarios de Windows, en el cuadro de texto **nombre de dominio de usuario externo de destino** , asegúrese de que el nombre de dominio de usuario externo destino esté especificado correctamente.

    ![Seleccionar base de datos de destino](../dma/media/select-target-database.png)

5. Seleccione **Siguiente**.

## <a name="select-schema-objects"></a>Seleccionar objetos de esquema

1. Seleccione los objetos de esquema de la base de datos de origen que desea migrar a Azure SQL Database.

    ![Seleccionar objetos de esquema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Some of the objects that cannot be converted as-is are presented with automatic fix opportunities. Clicking these objects on the left pane displays the suggested fixes on the right pane. Review the fixes and choose to either apply or ignore all changes, object by object. Note that applying or ignoring all changes for one object does not affect changes to other database objects. Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.

    ![Corrección sugerida](../dma/media/suggested-fix.png)

2. Seleccione **script SQL general**.

3. Revise el script generado.

    ![Script generado](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>Implementar esquema

1. Seleccione **implementar esquema**.

2. Revise los resultados de la implementación del esquema.

    ![Resultados de la implementación del esquema](../dma/media/schema-deployment-results.png)

3. Seleccione **migrar datos** para iniciar el proceso de migración de datos.

4. Seleccione las tablas con los datos que desea migrar.

    ![Seleccionar las tablas que se van a migrar](../dma/media/select-tables-to-migrate.png) 

5. Seleccione **Iniciar migración de datos**.

En la pantalla final se muestra el estado general.

   ![Estado de la migración](../dma/media/migration-status.png) 

## <a name="see-also"></a>Vea también

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Data Migration Assistant: opciones de configuración](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: procedimientos recomendados](../dma/dma-bestpractices.md)
