---
title: Migrar el servidor local de SQL (Asistente de migración de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c578625f9dac8b242dcd6d06fcf60925dd5b02c2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>Migrar mediante el Asistente de migración de datos local SQL Server

Este artículo proporciona instrucciones paso a paso para migrar SQL Server mediante el Asistente de migración de datos.

Asistente para migración de datos proporciona las migraciones a plataformas de datos de SQL Server y SQL Azure VM local moderna y evaluaciones sin problemas.  

Complete las tareas siguientes para llevar a cabo la migración.

- [Cree un nuevo proyecto de migración](#create-a-new-migration-project)
- [Especificar el origen y destino](#specify-source-and-target)
- [Agregar bases de datos](#add-databases)
- [Seleccione los inicios de sesión](#select-logins)

## <a name="create-a-new-migration-project"></a>Cree un nuevo proyecto de migración

1. Haga clic en **New** (+) en el panel izquierdo y seleccione la **migración** tipo de proyecto.

1. Establezca el tipo de servidor de origen y de destino en **SQL Server** si va a actualizar un servidor de SQL local a un moderno en SQL Server local.

1. Haga clic en **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar el origen y destino

1. Para el origen, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de origen** sección. 

1. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de origen.

1. Para el destino, escriba el nombre de instancia de SQL Server en el **nombre del servidor** campo el **detalles del servidor de destino** sección. 

1. Seleccione el **tipo de autenticación** admitidos por la instancia de SQL Server de destino.

1. Se recomienda cifrar la conexión seleccionando **cifrar conexión** en el **propiedades de conexión** sección.

1. Haga clic en **Siguiente**.

   ![Especificar la página de origen y de destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Agregar bases de datos

1. Elija las bases de datos específicos que se van a migrar seleccionando solo las bases de datos, en el panel izquierdo de la **agregar bases de datos** página.

   De forma predeterminada se seleccionan todas las bases de datos de usuario en la instancia de SQL Server de origen para la migración

1. Utilice la configuración de migración en el lado derecho de la página para establecer las opciones de migración que se aplican a las bases de datos, mediante los pasos siguientes.

   > [!NOTE]
   > Puede aplicar la configuración de migración para todas las bases de datos que está migrando, seleccionando el servidor en el panel izquierdo. También puede configurar una base de datos individual con una configuración específica, seleccione la base de datos en el panel izquierdo.


 1. Especifique el **compartido ubicación accesible por servidores de SQL de origen y destino para la operación de copia de seguridad**. Asegúrese de que la cuenta de servicio que se ejecuta el origen de SQL Server, instancia de tiene escribir privilegios en la ubicación compartida y la cuenta de servicio de destino con privilegios de lectura en la ubicación compartida.

 1. Especifique la ubicación para restaurar los datos y los archivos de registro transaccional en el servidor de destino.

    ![Agregar página de las bases de datos](../dma/media/AddDatabases.png)

1. Escriba una ubicación compartida que las instancias de SQL Server de origen y destino tienen acceso, en la **comparten opciones de ubicación** cuadro.

1. Si no puede proporcionar una ubicación compartida que servidores de SQL Server mediante el origen y de destino tienen acceso, seleccione **copiar las copias de seguridad de base de datos en una ubicación diferente que el servidor de destino pueda leer y restaurar a partir de**. A continuación, escriba un valor para el **ubicación para las copias de seguridad para la opción de restauración** cuadro. 

   Asegúrese de que la cuenta de usuario que ejecuta el Asistente de migración de datos con privilegios de lectura para la ubicación de copia de seguridad y privilegios de escritura en la ubicación desde la que se restaura el servidor de destino.

   ![Opción para copiar las copias de seguridad de base de datos en otra ubicación](../dma/media/CopyDatabaseDifferentLocation.png)

1. Haga clic en **Siguiente**.

Asistente para migración de datos realiza validaciones en las carpetas de copia de seguridad, datos y registro de ubicaciones de archivos. Si se produce un error en ninguna validación, corrija las opciones y haga clic en **siguiente**.

## <a name="select-logins"></a>Seleccione los inicios de sesión

1. Seleccione los inicios de sesión específicos para la migración.

   > [!IMPORTANT]
   > Asegúrese de seleccionar los inicios de sesión que están asignados a uno o más usuarios en las bases de datos seleccionados para la migración.   

   De forma predeterminada, se seleccionan los inicios de sesión de SQL Server y Windows que son aptos para la migración para la migración.

1. Haga clic en **Iniciar migración**.

   ![Seleccione los inicios de sesión e inicie la migración](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Ver los resultados

Puede supervisar el progreso de la migración en el **ver resultados** página.

![Página de vista de resultados](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados de la migración

1. Haga clic en **Exportar informe** en la parte inferior de la **ver resultados** página para guardar los resultados de la migración a un archivo CSV.

1. Revise el archivo guardado para obtener más información sobre la migración de inicio de sesión y, a continuación, compruebe los cambios.

## <a name="see-also"></a>Vea también

[Asistente de migración de datos (DMA)](../dma/dma-overview.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)

[Asistente de migración de datos: Prácticas recomendadas](../dma/dma-bestpractices.md)
