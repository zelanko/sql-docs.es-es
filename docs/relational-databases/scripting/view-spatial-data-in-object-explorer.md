---
title: Ver datos espaciales en el Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 6161c14a1baf87d2278dfa9a45cd67274a10c89d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39553985"
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
  
  
