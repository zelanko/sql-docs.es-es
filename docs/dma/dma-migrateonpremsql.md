---
title: Actualice SQL Server mediante el Data Migration Assistant
description: Aprenda a usar Data Migration Assistant para actualizar un SQL Server local a una versión posterior de SQL Server o a SQL Server en máquinas virtuales de Azure.
ms.custom: seo-lt-2019
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 00d27decc533d33056a7cc0cb19c2584fea564fb
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885873"
---
# <a name="upgrade-sql-server-using-the-data-migration-assistant"></a>Actualice SQL Server mediante el Data Migration Assistant

El Data Migration Assistant proporciona evaluaciones sin problemas de SQL Server locales y actualizaciones a versiones posteriores de SQL Server o migraciones a SQL Server en máquinas virtuales de Azure o Azure SQL Database.

En este artículo se proporcionan instrucciones paso a paso para actualizar SQL Server de forma local a versiones posteriores de SQL Server o a SQL Server en máquinas virtuales de Azure mediante el Data Migration Assistant.

## <a name="create-a-new-migration-project"></a>Creación de un proyecto de migración

1. En el panel izquierdo, seleccione **nuevo** (+) y, a continuación, el tipo de proyecto de **migración** .

2. Establezca el tipo de servidor de origen y de destino en **SQL Server** si va a actualizar un SQL Server local a una versión posterior de SQL Server local.

3. Seleccione **Crear**.

   ![Crear proyecto de migración](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Especificar el origen y el destino

1. En origen, escriba el nombre de la instancia de SQL Server en el campo **nombre del servidor** en la sección Detalles del **servidor de origen** . 

2. Seleccione el **tipo de autenticación** admitido por la instancia de SQL Server de origen.

3. En destino, escriba el nombre de la instancia de SQL Server en el campo **nombre del servidor** en la sección Detalles del **servidor de destino** . 

4. Seleccione el **tipo de autenticación** admitido por la instancia de SQL Server de destino.

5. Se recomienda cifrar la conexión seleccionando **cifrar conexión** en la sección **propiedades** de la conexión.

6. Haga clic en **Siguiente**.

   ![Especificar página de origen y de destino](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Agregar bases de datos

1. Elija las bases de datos específicas que desea migrar. para ello, solo tiene que seleccionar las bases de datos en el panel izquierdo de la página **Agregar bases de datos** .

   De forma predeterminada, se seleccionan todas las bases de datos de usuario en la instancia de SQL Server de origen para la migración.

2. Use la configuración de migración que se encuentra en el lado derecho de la página para establecer las opciones de migración que se aplican a las bases de datos. para ello, haga lo siguiente.

   > [!NOTE]
   > Puede aplicar la configuración de migración a todas las bases de datos que va a migrar, seleccionando el servidor en el panel izquierdo. También puede configurar una base de datos individual con valores específicos seleccionando la base de datos en el panel izquierdo.

    a. Especifique la **ubicación compartida a la que pueden acceder los servidores SQL de origen y de destino para la operación de copia de seguridad**. Asegúrese de que la cuenta de servicio que ejecuta la instancia de SQL Server de origen tiene privilegios de escritura en la ubicación compartida y que la cuenta de servicio de destino tiene privilegios de lectura en la ubicación compartida.

    b. Especifique la ubicación para restaurar los archivos de datos y de registro transaccionales en el servidor de destino.

    ![Página agregar bases de datos](../dma/media/AddDatabases.png)

3. Escriba una ubicación compartida a la que tengan acceso las instancias de SQL Server de origen y de destino, en el cuadro **Opciones de ubicación del recurso compartido** .

4. Si no puede proporcionar una ubicación compartida a la que los servidores SQL de origen y de destino tengan acceso, seleccione **copiar las copias de seguridad de base de datos en una ubicación diferente de la que el servidor de destino pueda leer y restaurar**. A continuación, escriba un valor para el cuadro **de opción ubicación de copias de seguridad para restaurar** . 

   Asegúrese de que la cuenta de usuario que ejecuta Data Migration Assistant tiene privilegios de lectura en la ubicación de copia de seguridad y privilegios de escritura en la ubicación desde la que restaura el servidor de destino.

   ![Opción para copiar copias de seguridad de base de datos en una ubicación diferente](../dma/media/CopyDatabaseDifferentLocation.png)

5. Seleccione **Next** (Siguiente).

El Data Migration Assistant realiza validaciones en las carpetas de copia de seguridad, los datos y las ubicaciones del archivo de registro. Si se produce un error en la validación, corrija las opciones y, a continuación, seleccione **siguiente**.

## <a name="select-logins"></a>Selección de inicios de sesión

1. Seleccione inicios de sesión específicos para la migración.

   > [!IMPORTANT]
   > Asegúrese de seleccionar los inicios de sesión asignados a uno o más usuarios en las bases de datos seleccionadas para la migración.   

   De forma predeterminada, se seleccionan todos los inicios de sesión de SQL Server y Windows que se pueden habilitar para la migración.

2. Seleccione **Iniciar migración**.

   ![Seleccionar inicios de sesión e iniciar la migración](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Vista de resultados

Puede supervisar el progreso de la migración en la página **ver resultados** .

![Página ver resultados](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportar resultados de migración

1. Haga clic en **exportar Informe** en la parte inferior de la página **ver resultados** para guardar los resultados de la migración en un archivo CSV.

2. Revise el archivo guardado para obtener más información acerca de la migración de inicio de sesión y, a continuación, compruebe los cambios.

## <a name="see-also"></a>Consulte también

- [Data Migration Assistant (DMA)](../dma/dma-overview.md)
- [Data Migration Assistant: opciones de configuración](../dma/dma-configurationsettings.md)
- [Data Migration Assistant: procedimientos recomendados](../dma/dma-bestpractices.md)
