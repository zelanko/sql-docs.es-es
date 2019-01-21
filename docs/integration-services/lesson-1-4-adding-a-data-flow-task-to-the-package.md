---
title: 'Paso 4: Incorporación de una tarea Flujo de datos al paquete | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f9bfb46276de6804aa9222a298bec96d970fd51
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143085"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>Lección 1-4: Incorporación de una tarea Flujo de datos al paquete

Después de haber creado los administradores de conexión para los datos de origen y destino, agregará una tarea Flujo de datos al paquete. La tarea Flujo de datos define el motor de flujo de datos que mueve los datos entre orígenes y destinos, y proporciona la funcionalidad para transformar, limpiar y modificar los datos a medida que se mueven. En la tarea de flujo de datos se lleva a cabo la mayor parte del proceso de extracción, transformación y carga (ETL).  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa el flujo de datos del flujo de control.  
  
## <a name="add-a-data-flow-task"></a>Incorporación de una tarea Flujo de datos  
  
1.  Seleccione la pestaña **Flujo de control**.  
  
2.  En el panel **Cuadro de herramientas de SSIS**, expanda **Favoritos** y arrastre una **tarea Flujo de datos** a la superficie de diseño de la pestaña **Flujo de control**.  
  
    > [!NOTE]  
    > Si el cuadro de herramientas de SSIS no está disponible, seleccione el menú **SSIS** y, luego, la opción **Cuadro de herramientas de SSIS** para mostrarla.  

3.  En la superficie de diseño de **Flujo de control**, haga clic con el botón derecho en la nueva **tarea Flujo de datos**, seleccione **Cambiar nombre** y cambie el nombre por **Extract Sample Currency Data**.  
  
    Proporcione nombres únicos para todos los componentes que agregue a una superficie de diseño. Para facilitar el uso y el mantenimiento, los nombres deben describir la función de cada componente. Seguir estas directrices de nomenclatura permite que los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sean autodocumentados. Los paquetes también pueden documentarse mediante anotaciones. Para más información sobre las anotaciones, consulte [Usar anotaciones en paquetes](../integration-services/use-annotations-in-packages.md).  
  
4.  Haga clic con el botón derecho en la tarea Flujo de datos, seleccione **Propiedades** y, en esta ventana, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 5: Incorporación y configuración del origen de archivo plano](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Vea también  
[Tarea Flujo de datos](../integration-services/control-flow/data-flow-task.md)  
  
  
  
