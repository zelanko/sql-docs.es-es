---
title: 'Tarea 8: Agregar un nuevo valor para la entidad estado en Excel | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 04ed80887a2a81a2179dcec423b9e22b3f9d43ef
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032036"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>Tarea 8: agregar un nuevo valor para la entidad Estado en Excel
  En esta tarea, agregará un valor para la entidad Estado en Excel y publicará el cambio en el servidor de MDS.  
  
1.  Agregar un **hoja de cálculo** en Excel, haga clic en la nueva pestaña en la parte inferior.  
  
     ![Excel - pestaña de hoja de cálculo nueva](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel - pestaña de hoja de cálculo nueva")  
  
2.  En **Excel**, haga clic en el **datos maestros** pestaña en el menú y, a continuación, haga clic en **Mostrar explorador** en la cinta de opciones.  
  
3.  En el **Explorador de datos maestros**, seleccione **proveedores** para **modelo**. Debe ver dos entidades: **Proveedor** y **estado** en la lista de entidades.  
  
4.  Haga doble clic en **estado** en la lista. Todos los miembros de la **estado** entidades de MDS deben mostrarse en la hoja de cálculo.  
  
5.  Ahora, agregue una fila al final con los valores siguientes: **Carolina del Norte** para **nombre** y **NC** para **código**. La codificación de colores distingue los registros nuevos y actualizados de los demás registros.  
  
     ![Excel - agregar North Carolina a estados](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - agregar North Carolina a Estados")  
  
6.  Haga clic en **publicar** en la cinta de opciones para publicar el cambio en MDS.  
  
     ![Excel - botón Publicar en la pestaña de datos maestros](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel - botón Publicar en la pestaña de datos maestros")  
  
7.  En el **publicar y anotar** diálogo cuadro, tenga en cuenta que el **usar la misma anotación para todos los cambios** está seleccionada. Aquí puede escribir una sola anotación para todos los cambios.  
  
8.  Seleccione **revisar los cambios y proporcionar anotaciones individualmente** opción para proporcionar una anotación para cada cambio (en este caso, sólo uno).  
  
     ![Excel: publicar y anotar el cuadro de diálogo](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "de Excel: publicar y anotar el cuadro de diálogo")  
  
9. Haga clic en **publicar** para publicar datos en MDS.  
  
10. Tenga en cuenta que **codificación en colores** para la fila con **Carolina del Norte** como el **estado** ahora es igual que otros registros.  
  
11. **Opcional:** Compruebe que el nuevo miembro (NC) se agrega a la **estado** entidad mediante el uso de la **Explorer** en **Master Data Manager**.  
  
12. En Excel, haga clic en el **estado** hoja de cálculo en la parte inferior y haga clic en **eliminar** para eliminar la hoja de cálculo. Al eliminar la hoja de cálculo no se eliminan los datos del servidor de MDS.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 9: Creación de una jerarquía derivada mediante Master Data Manager](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
