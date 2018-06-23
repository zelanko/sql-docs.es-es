---
title: 'Paso 4: Agregar una tarea Flujo de datos al paquete | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 29c42e491c6d36c20073a801051d8861d03ab0f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199733"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>Paso 4: agregar una tarea de flujo de datos al paquete
  Una vez que ha creado los administradores de conexión para los datos de origen y de destino, la siguiente tarea consiste en agregar una tarea de flujo de datos al paquete. La tarea de flujo de datos encapsula el motor de flujo de datos que mueve datos entre orígenes y destinos, y proporciona la funcionalidad para transformar, limpiar y modificar los datos a medida que se mueven. En la tarea de flujo de datos se lleva a cabo la mayor parte del proceso de extracción, transformación y carga (ETL).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa el flujo de datos de flujo de control.  
  
### <a name="to-add-a-data-flow-task"></a>Para agregar una tarea de flujo de datos  
  
1.  Haga clic en la pestaña **Flujo de control** .  
  
2.  En el **Cuadro de herramientas de SSIS**, expanda **Favoritos**y arrastre una **tarea Flujo de datos** a la superficie de diseño de la pestaña **Flujo de control** .  
  
    > [!NOTE]  
    >  Si el cuadro de herramientas de SSIS no está disponible, en el menú principal seleccione SSIS y después el cuadro de herramientas de SSIS para mostrar el cuadro de herramientas de SSIS.  
  
3.  En el **flujo de Control** superficie de diseño, haga clic en el recién agregado **tarea flujo de datos**, haga clic en **cambiar el nombre de**y cambie el nombre a `Extract Sample Currency Data`.  
  
     Es aconsejable proporcionar nombres únicos a todos los componentes que se agregan a una superficie de diseño. Para facilitar su uso y mantenimiento, los nombres deben describir la función que lleva a cabo cada componente. Seguir estas directrices de nomenclatura permite que los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sean autodocumentados. Los paquetes también pueden documentarse mediante anotaciones. Para obtener más información sobre cómo usar anotaciones, consulte [Usar anotaciones en paquetes](use-annotations-in-packages.md).  
  
4.  Haga clic en la tarea flujo de datos, haga clic en **propiedades**y en la ventana Propiedades, compruebe que la `LocaleID` propiedad está establecida en **inglés (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 5: Agregar y configurar el origen de archivo plano](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Vea también  
 [Tarea Flujo de datos](control-flow/data-flow-task.md)  
  
  