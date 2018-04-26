---
title: Ver datos espaciales en el Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4172a48b28cf2b38a9da335caf18c5a60dd21876
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="view-spatial-data-in-object-explorer"></a>Ver datos espaciales en el Explorador de objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  La ventana **Resultados espaciales** del Editor de consultas proporciona herramientas de asignación visual para ver los resultados de los datos espaciales junto con los datos mostrados en formato de cuadrícula en la ventana **Resultados** . Para mostrar datos espaciales en la ventana **Resultados espaciales** , los resultados de la consulta deben contener al menos una columna de datos espaciales con datos de geometría o de geografía.  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>Para ver datos espaciales en la ventana de resultados espaciales  
  
1.  En el Editor de consultas, haga clic en la pestaña **Resultados espaciales** .  
  
    > [!NOTE]  
    >  Esta ventana no está disponible si los resultados de la consulta no contienen datos espaciales o si se especifica que los resultados se devuelvan como texto.  
  
2.  Seleccione la columna que desea ver en la lista **Seleccionar columna espacial** . Si solo hay una columna espacial en la tabla, esta columna es la opción predeterminada en la lista.  
  
3.  Seleccione la columna no espacial que quiere usar como etiquetas de datos en la lista **Seleccionar columna de etiqueta** .  
  
4.  Seleccione la proyección que desea para los datos de geografía en la lista **Seleccionar proyección** . La proyección predeterminada es Equirectangular; otras proyecciones disponibles son Mercator, Robinson o Bonne.  
  
    > [!NOTE]  
    >  **Seleccionar proyección** no está disponible si la columna espacial contiene datos de geometría.  
  
5.  Ajuste el control deslizante **Zoom** para aumentar el tamaño visual de los elementos asignados. En las formas de polígono, la etiqueta solo está visible cuando la forma es lo suficientemente grande como para contener el texto del rótulo.  
  
## <a name="see-also"></a>Ver también  
 [Ventana Resultados espaciales](../../relational-databases/scripting/spatial-results-window.md)   
 [Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
