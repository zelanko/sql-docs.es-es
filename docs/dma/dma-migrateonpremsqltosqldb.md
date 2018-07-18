---
title: Migrar en SQL Server local a Azure SQL Database mediante Data Migration Assistant | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar un servidor de SQL en el entorno local a Azure SQL Database
ms.custom: ''
ms.date: 07/09/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 5de33f3a78a68f0afac0ead0d42b244cc78a85ad
ms.sourcegitcommit: dcd29cd2d358bef95652db71f180d2a31ed5886b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2018
ms.locfileid: "37935842"
---
# <a name="migrate-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>Migración local de SQL Server a SQL Server o SQL Server en máquinas virtuales de Azure mediante Data Migration Assistant

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
   > Es recommedned que cifrar la conexión seleccionando el **cifrar conexión** casilla de verificación bajo **poperties conexión**.

    ![Seleccione el servidor de origen](../dma/media/select-source-server.png)

3. Seleccione **Conectar**.

4. Seleccione una base de datos de origen único para migrar a Azure SQL Database.

   > [!NOTE]
   > Si desea evaluar la base de datos y la vista y aplicar recomienda correcciones antes de la migración, seleccione el **base de datos de evaluación antes de la migración?** casilla de verificación.

    ![Seleccione la base de datos de origen](../dma/media/select-source-database.png)

5. Seleccione **Siguiente**.

## <a name="specify-the-target-server-and-database"></a>Especifique el servidor de destino y la base de datos

1. Para el destino, en **conectar al servidor de destino**, en el **nombre del servidor** texto, escriba el nombre de la instancia de Azure SQL Database. 

2. Seleccione el **tipo de autenticación** admitidos por la instancia de Azure SQL Database de destino.

   > [!NOTE]
   > Es recommedned que cifrar la conexión seleccionando el **cifrar conexión** casilla de verificación bajo **poperties conexión**.

     ![Seleccione el servidor de destino](../dma/media/select-target-server.png)

3. Seleccione **Conectar**.

4. Seleccione una base de datos de destino único que se va a migrar.

   > [!NOTE]
   > Si va a migrar usuarios de Windows, en el **nombre de dominio de usuario externo de destino** texto cuadro, asegúrese de que el nombre de dominio de usuario externo de destino se ha especificado correctamente.

    ![Seleccione la base de datos de destino](../dma/media/select-target-database.png)

5. Seleccione **Siguiente**.

## <a name="select-schema-objects"></a>Seleccione los objetos de esquema

1.  Seleccione los objetos de esquema de la base de datos de origen que desea migrar a Azure SQL Database.

    ![Seleccione los objetos de esquema](../dma/media/select-schema-objects.png)

       > [!NOTE]
       > Algunos de los objetos que no se puede convertir como-es familiarizarse con la corrección automática. Al hacer clic en estos objetos en el panel izquierdo muestra las correcciones sugeridas en el panel derecho. Revise las correcciones y optar por aplicar o ignorar todos los cambios de objeto. Tenga en cuenta que aplicar o ignorar todos los cambios de un objeto no afecta a los cambios a otros objetos de base de datos. Las instrucciones que no se pueden convertir o corregidas automáticamente se reproduce a la base de datos de destino y un comentario.

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

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
- [Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)
