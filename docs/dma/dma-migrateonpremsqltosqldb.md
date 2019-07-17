---
title: Migrar un entorno local SQL Server o SQL Server en máquinas virtuales de Azure a Azure SQL Database mediante Data Migration Assistant | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar un servidor de SQL en el entorno local a Azure SQL Database
ms.custom: ''
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
ms.openlocfilehash: 37e0065ed711c3cf550fec4bafe9aa08be8398e6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262313"
---
# <a name="migrate-on-premises-sql-server-or-sql-server-on-azure-vms-to-azure-sql-database-using-the-data-migration-assistant"></a>Migrar un entorno local SQL Server o SQL Server en máquinas virtuales de Azure a Azure SQL Database mediante Data Migration Assistant

Data Migration Assistant proporciona evaluaciones sin problemas de SQL Server local y las actualizaciones a las versiones posteriores de SQL Server o migraciones de SQL Server en máquinas virtuales de Azure o Azure SQL Database.

En este artículo proporciona instrucciones paso a paso para migrar SQL Server local a Azure SQL Database mediante Data Migration Assistant.

## <a name="create-a-new-migration-project"></a>Cree un nuevo proyecto de migración

1. En el panel izquierdo, seleccione **New** (+) y, a continuación, seleccione el **migración** tipo de proyecto.

2. Establece el tipo de origen en **SQL Server** y escriba en el servidor de destino **Azure SQL Database**.

3. Seleccione **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate1.png)

## <a name="specify-the-source-server-and-database"></a>Especifique el servidor de origen y la base de datos

1. Para el origen, en **conectar al servidor de origen**, en el **nombre del servidor** texto, escriba el nombre de la instancia de SQL Server de origen.

2. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de origen.

   > [!NOTE]
   > Se recomienda cifrar la conexión seleccionando el **cifrar conexión** casilla de verificación bajo **poperties conexión**.

    ![Seleccione el servidor de origen](../dma/media/select-source-server.png)

3. Seleccione **Conectar**.

4. Seleccione una base de datos de origen único para migrar a Azure SQL Database.

   > [!NOTE]
   > Si desea evaluar la base de datos y la vista y aplicar recomienda correcciones antes de la migración, seleccione el **base de datos de evaluación antes de la migración?** casilla de verificación.

    ![Seleccione la base de datos de origen](../dma/media/select-source-database.png)

5. Seleccione **Next** (Siguiente).

## <a name="specify-the-target-server-and-database"></a>Especifique el servidor de destino y la base de datos

1. Para el destino, en **conectar al servidor de destino**, en el **nombre del servidor** texto, escriba el nombre de la instancia de Azure SQL Database. 

2. Seleccione el **tipo de autenticación** admitidos por la instancia de Azure SQL Database de destino.

   > [!NOTE]
   > Se recomienda cifrar la conexión seleccionando el **cifrar conexión** casilla de verificación bajo **poperties conexión**.

     ![Seleccione el servidor de destino](../dma/media/select-target-server.png)

3. Seleccione **Conectar**.

4. Seleccione una base de datos de destino único que se va a migrar.

   > [!NOTE]
   > Si va a migrar usuarios de Windows, en el **nombre de dominio de usuario externo de destino** texto cuadro, asegúrese de que el nombre de dominio de usuario externo de destino se ha especificado correctamente.

    ![Seleccione la base de datos de destino](../dma/media/select-target-database.png)

5. Seleccione **Next** (Siguiente).

## <a name="select-schema-objects"></a>Seleccione los objetos de esquema

1. Seleccione los objetos de esquema de la base de datos de origen que desea migrar a Azure SQL Database.

    ![Seleccione los objetos de esquema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Some of the objects that cannot be converted as-is are presented with automatic fix opportunities. Clicking these objects on the left pane displays the suggested fixes on the right pane. Review the fixes and choose to either apply or ignore all changes, object by object. Note that applying or ignoring all changes for one object does not affect changes to other database objects. Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.

    ![Corrección sugerida](../dma/media/suggested-fix.png)

2. Seleccione **secuencia de comandos SQL General**.

3. Revise el script generado.

    ![Script generado](../dma/media/generated-script.png)

## <a name="deploy-schema"></a>Implementar esquema

1. Seleccione **implementar esquema**.

2. Revise los resultados de la implementación del esquema.

    ![Resultados de la implementación de esquema](../dma/media/schema-deployment-results.png)

3. Seleccione **migrar datos** para iniciar el proceso de migración de datos.

4. Seleccione las tablas con los datos que desea migrar.

    ![Seleccionar las tablas de migración](../dma/media/select-tables-to-migrate.png) 

5. Seleccione **Iniciar migración de datos**.

La pantalla final muestra el estado general.

   ![Estado de la migración](../dma/media/migration-status.png) 

## <a name="see-also"></a>Vea también

* [Data Migration Assistant (DMA)](../dma/dma-overview.md)
* [Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
* [Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)
