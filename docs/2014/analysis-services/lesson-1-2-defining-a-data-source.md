---
title: Definir un origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f764d7e7640fc7549d97402a83f997b63f9105cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179082"
---
# <a name="defining-a-data-source"></a>Definir un origen de datos
  Tras crear un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], generalmente se empieza a trabajar con el mismo definiendo uno o más orígenes de datos que el proyecto usará. Al definir un origen de datos, se define la información de cadena de conexión que se utilizará para establecer la conexión con el origen de datos. Para más información, vea [Crear un origen de datos &#40;SSAS multidimensional&#41;](multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 En la tarea siguiente, definirá la base de datos de ejemplo AdventureWorksDWSQLServer2012 como origen de datos para el proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . En el caso de este tutorial, esta base de datos se encuentra en el equipo local; no obstante, las bases de datos de origen generalmente se encuentran hospedadas en uno o más equipos remotos.  
  
### <a name="to-define-a-new-data-source"></a>Para definir un origen de datos nuevo  
  
1.  En el Explorador de soluciones (a la derecha de la ventana de Microsoft Visual Studio), haga clic con el botón derecho en **Orígenes de datos**y, después, haga clic en **Nuevo origen de datos**.  
  
2.  En la página de **inicio** del **Asistente para orígenes de datos**, haga clic en **Siguiente** para abrir la página **Seleccionar cómo definir la conexión** .  
  
3.  En la página **Seleccionar cómo definir la conexión** , puede definir un origen de datos basado en una conexión nueva, en una conexión existente o en un objeto de origen de datos definido con anterioridad. En este tutorial, va a definir un origen de datos basado en una conexión nueva. Compruebe que la opción **Crear un origen de datos basado en una conexión nueva o existente** está seleccionada y después haga clic en **Nueva**.  
  
4.  En el cuadro de diálogo **Administrador de conexiones** se definen las propiedades de conexión para el origen de datos. En el cuadro de lista **Proveedor** , compruebe que está seleccionada la opción **Native OLE DB\SQL Server Native Client 11.0** .  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] también admite otros proveedores, que se muestran en la lista **Proveedor** .  
  
5.  En el **nombre del servidor** cuadro de texto, escriba `localhost`.  
  
     Para conectarse a una instancia con nombre en el equipo local, escriba **localhost\\< nombre de instancia\>**. Para conectarse al equipo especificado en lugar de al equipo local, escriba el nombre del equipo o la dirección IP.  
  
6.  Compruebe que la opción **Usar autenticación de Windows** está seleccionada. En la lista **Seleccione o escriba un nombre de base de datos** , seleccione **AdventureWorksDW2012**.  
  
7.  Haga clic en **Probar conexión** para probar la conexión a la base de datos.  
  
8.  Haga clic en **Aceptar**y, a continuación, en **Siguiente**.  
  
9. En la página **Información de suplantación** del asistente, debe definir las credenciales de seguridad que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] debe usar para conectarse al origen de datos. La suplantación afecta a la cuenta de Windows usada para conectarse al origen de datos cuando está seleccionada la autenticación de Windows. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no admite la suplantación para el procesamiento de objetos OLAP. Seleccione **Usar cuenta de servicio**y haga clic en **Siguiente**.  
  
10. En la página **Finalización del asistente** , acepte el nombre predeterminado **Adventure Works DW 2012**y, después, haga clic en **Finalizar** para crear el nuevo origen de datos.  
  
> [!NOTE]  
>  Para modificar las propiedades del origen de datos una vez creado, haga doble clic en el origen de datos en la carpeta **Orígenes de datos** para mostrar las propiedades del origen de datos en el **Diseñador de origen de datos**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Definir una vista del origen de datos](lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un origen de datos &#40;SSAS Multidimensional&#41;](multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
