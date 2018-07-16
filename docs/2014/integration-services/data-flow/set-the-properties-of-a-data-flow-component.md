---
title: Establecer las propiedades de un componente de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], properties
ms.assetid: 73000ef6-52a2-4dec-8320-0e79acf0c2c5
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 61c56e88ef2124e2c8483ecaff778496840de2d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190835"
---
# <a name="set-the-properties-of-a-data-flow-component"></a>Establecer las propiedades de un componente de flujo de datos
  Para establecer las propiedades de los componentes de flujo de datos, que incluyen orígenes, destinos y transformaciones, utilice una de las características siguientes:  
  
-   Los editores de componentes que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona. Estos editores incluyen solo las propiedades personalizadas de cada componente de flujo de datos.  
  
-   La ventana **Propiedades** enumera las propiedades personalizadas de nivel de componente de cada elemento, al igual que las propiedades que son comunes a todos los elementos de flujo de datos.  
  
-   El cuadro de diálogo **Editor avanzado** proporciona acceso a las propiedades personalizadas de cada componente. El cuadro de diálogo **Editor avanzado** también permite el acceso a las propiedades comunes a todos los componentes de flujo de datos: propiedades de entradas, salidas, salidas de errores, columnas y columnas externas.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-a-component-editor"></a>Para establecer las propiedades de un componente de flujo de datos mediante un editor de componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el flujo de datos con el componente cuyas propiedades quiere ver y modificar.  
  
4.  Haga doble clic en el componente de flujo de datos.  
  
5.  En el editor de componentes, vea o modifique los valores de las propiedades y luego cierre el editor.  
  
6.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-properties-window"></a>Para establecer las propiedades de un componente de flujo de datos mediante una ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el componente cuyas propiedades quiere ver y modificar.  
  
4.  Haga clic con el botón derecho en el componente de flujo de datos y luego haga clic en **Propiedades**.  
  
5.  Vea o modifique los valores de la propiedad y luego cierre la ventana **Propiedades** .  
  
    > [!NOTE]  
    >  Muchas propiedades son de solo lectura y no pueden modificarse.  
  
6.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
### <a name="to-set-the-properties-of-a-data-flow-component-by-using-the-advanced-editor"></a>Para establecer las propiedades de un componente de flujo de datos mediante el Editor avanzado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el componente que quiere ver o modificar.  
  
4.  En el diseñador de flujos de datos, haga clic con el botón derecho en el componente de flujo de datos y luego haga clic en **Mostrar editor avanzado**.  
  
    > [!NOTE]  
    >  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los componentes de flujo de datos que admiten varias entradas no pueden usar el **Editor avanzado**.  
  
5.  En el cuadro de diálogo **Editor avanzado** , realice cualquiera de los pasos siguientes:  
  
    -   Para ver y especificar la conexión que el componente utiliza, haga clic en la pestaña **Administradores de conexiones** .  
  
        > [!NOTE]  
        >  La pestaña **Administradores de conexiones** está disponible solamente para los componentes de flujo de datos que usan administradores de conexiones para conectarse a orígenes de datos como archivos y bases de datos  
  
    -   Para ver y modificar propiedades de nivel de componente, haga clic en la pestaña **Propiedades de componente** .  
  
    -   Para ver y modificar asignaciones entre columnas externas y la salida disponible, haga clic en la pestaña **Asignaciones de columnas** .  
  
        > [!NOTE]  
        >  La pestaña **Asignaciones de columnas** solo está disponible al ver o editar orígenes o destinos.  
  
    -   Para ver una lista de las columnas de entrada disponibles y para actualizar los nombres de las columnas de salida, haga clic en la pestaña **Columnas de entrada** .  
  
        > [!NOTE]  
        >  La pestaña Columnas de entrada está disponible solamente cuando se trabaja con transformaciones o destinos. Para más información, consulte [Integration Services Transformations](transformations/integration-services-transformations.md).  
  
    -   Para ver y modificar las propiedades de las entradas, salidas y salidas de errores, y las propiedades de las columnas que contienen, haga clic en la pestaña **Propiedades de entrada y salida** .  
  
        > [!NOTE]  
        >  Los orígenes no tienen entradas. Los destinos no tienen salidas, excepto una salida de errores opcional.  
  
6.  Vea o modifique los valores de propiedades.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## <a name="see-also"></a>Vea también  
 [Transformaciones de Integration Services](transformations/integration-services-transformations.md)  
  
  
