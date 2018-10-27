---
title: Actualización en SQL Server local a SQL Server o SQL Server en máquinas virtuales de Azure mediante Data Migration Assistant | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para actualizar un servidor de SQL en el entorno local a una versión posterior de SQL Server o a SQL Server en máquinas virtuales de Azure
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: e0d3ee1784653205feb4aa95a80a82d5ac27ec46
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643843"
---
# <a name="upgrade-on-premises-sql-server-to-sql-server-or-sql-server-on-azure-vms-using-the-data-migration-assistant"></a>Actualización local de SQL Server a SQL Server o SQL Server en máquinas virtuales de Azure mediante Data Migration Assistant

Data Migration Assistant proporciona evaluaciones sin problemas de SQL Server local y las actualizaciones a las versiones posteriores de SQL Server o migraciones de SQL Server en máquinas virtuales de Azure o Azure SQL Database.

Este artículo proporciona instrucciones paso a paso para actualizar SQL Server local a una versión posterior de SQL Server o SQL Server en máquinas virtuales de Azure mediante Data Migration Assistant.   

## <a name="create-a-new-migration-project"></a>Cree un nuevo proyecto de migración

1. En el panel izquierdo, seleccione **New** (+) y, a continuación, el **migración** tipo de proyecto.

2. Establece el tipo de servidor de origen y destino en **SQL Server** si va a actualizar un servidor de SQL en el entorno local a una versión posterior de un entorno local de SQL Server.

3. Seleccione **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar el origen y destino

1. Para el origen, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de origen** sección. 

2. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de origen.

3. Para el destino, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de destino** sección. 

4. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de destino.

5. Se recomienda cifrar la conexión seleccionando **cifrar conexión** en el **las propiedades de conexión** sección.

6. Haga clic en **Siguiente**.

   ![Especificar la página de origen y destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Agregar bases de datos

1. Elija las bases de datos específicas que desea migrar seleccionando solo esas bases de datos, en el panel izquierdo de la **agregar bases de datos** página.

   De forma predeterminada se seleccionan todas las bases de datos de usuario en la instancia de SQL Server de origen para la migración

2. Use la configuración de migración en el lado derecho de la página para establecer las opciones de migración que se aplican a las bases de datos, mediante los pasos siguientes.

   > [!NOTE]
   > Puede aplicar la configuración de migración para todas las bases de datos que se va a migrar, seleccionando el servidor en el panel izquierdo. También puede configurar una base de datos individual con una configuración específica, seleccione la base de datos en el panel izquierdo.

    A. Especifique el **comparten ubicación accesible por los servidores SQL de origen y destino para la operación de copia de seguridad**. Asegúrese de que la cuenta de servicio que ejecuta el origen tiene la instancia de SQL Server escribir privilegios en la ubicación compartida y la cuenta de servicio de destino con privilegios de lectura en la ubicación compartida.

    B. Especifique la ubicación para restaurar los datos y archivos de registro transaccional en el servidor de destino.

    ![Agregar página de las bases de datos](../dma/media/AddDatabases.png)

3. Escriba una ubicación compartida que las instancias de SQL Server de origen y destino tienen acceso, en el **comparten ubicación opciones** cuadro.

4. Si no puede proporcionar una ubicación compartida que servidores SQL de origen y destino tienen acceso, seleccione **copiar las copias de seguridad de base de datos en una ubicación diferente que el servidor de destino pueda leer y restaurar desde**. A continuación, escriba un valor para el **ubicación para las copias de seguridad para la opción de restauración** cuadro. 

   Asegúrese de que la cuenta de usuario que ejecuta Data Migration Assistant con privilegios de lectura para la ubicación de copia de seguridad y privilegios de escritura en la ubicación desde la que se restaura el servidor de destino.

   ![Opción para copiar las copias de seguridad de base de datos en otra ubicación](../dma/media/CopyDatabaseDifferentLocation.png)

5. Seleccione **Siguiente**.

Data Migration Assistant realiza comprobaciones en las carpetas de copia de seguridad, datos y ubicaciones de archivos de registro. Si se produce un error de validación, corregir las opciones y, a continuación, seleccione **siguiente**.

## <a name="select-logins"></a>Seleccione los inicios de sesión

1. Seleccione los inicios de sesión específicos para la migración.

   > [!IMPORTANT]
   > Asegúrese de seleccionar los inicios de sesión que se asignan a los usuarios de una o varias de las bases de datos seleccionadas para la migración.   

   De forma predeterminada, se seleccionan los inicios de sesión de SQL Server y Windows que cumplen los requisitos para la migración para la migración.

2. Seleccione **Iniciar migración**.

   ![Seleccione los inicios de sesión e iniciar la migración](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Ver los resultados

Puede supervisar el progreso de la migración en el **ver resultados** página.

![Página de resultados de vista](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados de la migración

1. Haga clic en **Exportar informe** en la parte inferior de la **ver resultados** página para guardar los resultados de la migración a un archivo CSV.

2. Revise el archivo guardado para obtener más información sobre la migración de inicio de sesión y, a continuación, comprobar los cambios.

## <a name="see-also"></a>Vea también

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
- [Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)
