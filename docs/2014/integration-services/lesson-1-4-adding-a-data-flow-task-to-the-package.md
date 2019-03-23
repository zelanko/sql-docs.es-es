---
title: 'Paso 4: Adición de una tarea Flujo de datos al paquete | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 542b7e3ffcc4a1db5b2053c840b785f775384fe1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381193"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>Paso 4: Agregar una tarea de flujo de datos al paquete
  Una vez que ha creado los administradores de conexión para los datos de origen y de destino, la siguiente tarea consiste en agregar una tarea de flujo de datos al paquete. La tarea de flujo de datos encapsula el motor de flujo de datos que mueve datos entre orígenes y destinos, y proporciona la funcionalidad para transformar, limpiar y modificar los datos a medida que se mueven. En la tarea de flujo de datos se lleva a cabo la mayor parte del proceso de extracción, transformación y carga (ETL).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa el flujo de datos del flujo de control.  
  
### <a name="to-add-a-data-flow-task"></a>Para agregar una tarea de flujo de datos  
  
1.  Haga clic en la pestaña **Flujo de control** .  
  
2.  En el **Cuadro de herramientas de SSIS**, expanda **Favoritos**y arrastre una **tarea Flujo de datos** a la superficie de diseño de la pestaña **Flujo de control** .  
  
    > [!NOTE]  
    >  Si el cuadro de herramientas de SSIS no está disponible, seleccione SSIS en el menú principal y, después, haga clic en el cuadro de herramientas de SSIS para mostrarlo.  
  
3.  En el **flujo de Control** superficie de diseño, haga clic en la recién agregada **Data Flow Task**, haga clic en **cambiar el nombre de**y cambie el nombre a `Extract Sample Currency Data`.  
  
     Es aconsejable proporcionar nombres únicos a todos los componentes que se agregan a una superficie de diseño. Para facilitar su uso y mantenimiento, los nombres deben describir la función que lleva a cabo cada componente. Seguir estas directrices de nomenclatura permite que los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sean autodocumentados. Los paquetes también pueden documentarse mediante anotaciones. Para obtener más información sobre cómo usar anotaciones, consulte [Usar anotaciones en paquetes](use-annotations-in-packages.md).  
  
4.  Haga clic en la tarea flujo de datos, haga clic en **propiedades**y en la ventana Propiedades, compruebe que la `LocaleID` propiedad está establecida en **inglés (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 5: Agregar y configurar el origen de archivo plano](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Vea también  
 [tarea Flujo de datos](control-flow/data-flow-task.md)  
  
  
