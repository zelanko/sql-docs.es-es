---
title: Migrar un servidor SQL en el entorno local con Data Migration Assistant | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar un servidor de SQL en el entorno local a otro servidor SQL Server o a Azure SQL Database
ms.custom: ''
ms.date: 09/01/2017
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
ms.openlocfilehash: 8133b4176fc8f8197cab646d51f4ece68b6250bc
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784816"
---
# <a name="migrate-an-on-premises-sql-server-with-data-migration-assistant"></a>Migrar un servidor SQL en el entorno local con Data Migration Assistant

En este artículo proporciona instrucciones paso a paso para migrar SQL Server mediante Data Migration Assistant. Asistente para migración de datos proporciona evaluaciones sin problemas y las migraciones a plataformas de datos de SQL Server y SQL Azure VM modernas de forma local y a Azure SQL Database.  

Para realizar la migración, complete las tareas siguientes.

- [Cree un nuevo proyecto de migración](#create-a-new-migration-project)
- [Especificar el origen y destino](#specify-source-and-target)
- [Agregar bases de datos](#add-databases)
- [Seleccione los inicios de sesión](#select-logins)

## <a name="create-a-new-migration-project"></a>Cree un nuevo proyecto de migración

1. Haga clic en **New** (+) en el panel izquierdo y seleccione el **migración** tipo de proyecto.

1. Establece el tipo de servidor de origen y destino en **SQL Server** si va a actualizar un servidor de SQL en el entorno local a una moderna en SQL Server local.

1. Haga clic en **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar el origen y destino

1. Para el origen, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de origen** sección. 

1. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de origen.

1. Para el destino, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de destino** sección. 

1. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de destino.

1. Se recomienda cifrar la conexión seleccionando **cifrar conexión** en el **las propiedades de conexión** sección.

1. Haga clic en **Siguiente**.

   ![Especificar la página de origen y destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Agregar bases de datos

1. Elija las bases de datos específicas que desea migrar seleccionando solo esas bases de datos, en el panel izquierdo de la **agregar bases de datos** página.

   De forma predeterminada se seleccionan todas las bases de datos de usuario en la instancia de SQL Server de origen para la migración

1. Use la configuración de migración en el lado derecho de la página para establecer las opciones de migración que se aplican a las bases de datos, mediante los pasos siguientes.

   > [!NOTE]
   > Puede aplicar la configuración de migración para todas las bases de datos que se va a migrar, seleccionando el servidor en el panel izquierdo. También puede configurar una base de datos individual con una configuración específica, seleccione la base de datos en el panel izquierdo.

 1. Especifique el **comparten ubicación accesible por los servidores SQL de origen y destino para la operación de copia de seguridad**. Asegúrese de que la cuenta de servicio que ejecuta el origen tiene la instancia de SQL Server escribir privilegios en la ubicación compartida y la cuenta de servicio de destino con privilegios de lectura en la ubicación compartida.

 1. Especifique la ubicación para restaurar los datos y archivos de registro transaccional en el servidor de destino.

    ![Agregar página de las bases de datos](../dma/media/AddDatabases.png)

1. Escriba una ubicación compartida que las instancias de SQL Server de origen y destino tienen acceso, en el **comparten ubicación opciones** cuadro.

1. Si no puede proporcionar una ubicación compartida que servidores SQL de origen y destino tienen acceso, seleccione **copiar las copias de seguridad de base de datos en una ubicación diferente que el servidor de destino pueda leer y restaurar desde**. A continuación, escriba un valor para el **ubicación para las copias de seguridad para la opción de restauración** cuadro. 

   Asegúrese de que la cuenta de usuario que ejecuta Data Migration Assistant con privilegios de lectura para la ubicación de copia de seguridad y privilegios de escritura en la ubicación desde la que se restaura el servidor de destino.

   ![Opción para copiar las copias de seguridad de base de datos en otra ubicación](../dma/media/CopyDatabaseDifferentLocation.png)

1. Haga clic en **Siguiente**.

Asistente para migración de datos realiza las validaciones en las carpetas de copia de seguridad, datos y registro de ubicaciones de archivos. Si se produce un error de validación, corrija las opciones y haga clic en **siguiente**.

## <a name="select-logins"></a>Seleccione los inicios de sesión

1. Seleccione los inicios de sesión específicos para la migración.

   > [!IMPORTANT]
   > Asegúrese de seleccionar los inicios de sesión que se asignan a los usuarios de una o varias de las bases de datos seleccionadas para la migración.   

   De forma predeterminada, se seleccionan los inicios de sesión de SQL Server y Windows que cumplen los requisitos para la migración para la migración.

1. Haga clic en **Iniciar migración**.

   ![Seleccione los inicios de sesión e iniciar la migración](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Ver los resultados

Puede supervisar el progreso de la migración en el **ver resultados** página.

![Página de resultados de vista](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados de la migración

1. Haga clic en **Exportar informe** en la parte inferior de la **ver resultados** página para guardar los resultados de la migración a un archivo CSV.

1. Revise el archivo guardado para obtener más información sobre la migración de inicio de sesión y, a continuación, comprobar los cambios.

## <a name="see-also"></a>Vea también

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)

[Asistente para la migración de datos: Procedimientos recomendados](../dma/dma-bestpractices.md)
