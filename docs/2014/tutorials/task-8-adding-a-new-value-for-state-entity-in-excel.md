---
title: 'Tarea 8: agregar un nuevo valor para la entidad estado en Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 831d0b504a65d485413772ee3711e689e29ee2a3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489706"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>Tarea 8: Adición de un nuevo valor para la entidad Estado en Excel
  En esta tarea, agregará un valor para la entidad Estado en Excel y publicará el cambio en el servidor de MDS.  
  
1.  Para agregar una **hoja de trabajo** en Excel, haga clic en la pestaña nuevo de la parte inferior.  
  
     ![Excel - Pestaña Nueva hoja de cálculo](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - Pestaña Nueva hoja de cálculo")  
  
2.  En **Excel**, haga clic en la pestaña **datos maestros** del menú y, a continuación, haga clic en **Mostrar explorador** en la cinta de opciones.  
  
3.  En el **Explorador de datos maestro**, seleccione **proveedores** en **modelo**. Debería ver dos entidades: **proveedor** y **Estado** en la lista de entidades.  
  
4.  Haga doble clic en **Estado** en la lista. Todos los miembros de la entidad **State** de MDS deben mostrarse en la hoja de cálculo.  
  
5.  Ahora, agregue una fila al final con los siguientes valores: **Carolina del norte** para **nombre** y **NC** para el **código**. La codificación de colores distingue los registros nuevos y actualizados de los demás registros.  
  
     ![Excel - Agregar North Carolina a Estados](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - Agregar North Carolina a Estados")  
  
6.  Haga clic en **publicar** en la cinta de opciones para publicar el cambio en MDS.  
  
     ![Excel - Botón Publicar en la pestaña de datos maestros](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - Botón Publicar en la pestaña de datos maestros")  
  
7.  En el cuadro de diálogo **publicar y anotar** , observe que está seleccionada la opción **usar la misma anotación para todos los cambios** . Aquí puede escribir una sola anotación para todos los cambios.  
  
8.  Seleccione la opción **Revisar cambios y proporcionar anotaciones individualmente** para proporcionar una anotación para cada cambio (en este caso, solo uno).  
  
     ![Excel - Cuadro de diálogo Publicar y anotar](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel - Cuadro de diálogo Publicar y anotar")  
  
9. Haga clic en **publicar** para publicar datos en MDS.  
  
10. Observe que la **codificación de colores** de la fila con el norte de **Carolina** como el **Estado** es la misma que la de otros registros.  
  
11. **Opcional:** Compruebe que el nuevo miembro (NC) se agrega a la entidad **Estado** mediante el **Explorador** de **Master Data Manager**.  
  
12. En Excel, haga clic con el botón secundario en la hoja de cálculo de **Estado** en la parte inferior y haga clic en **eliminar** para eliminar la hoja de cálculo. Al eliminar la hoja de cálculo no se eliminan los datos del servidor de MDS.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 9: Creación de una jerarquía derivada mediante Master Data Manager](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
