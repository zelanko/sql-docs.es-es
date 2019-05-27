---
title: Ventana Resultados espaciales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2d5a477-6496-4d01-adee-7322ebdfadf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 606ac348ce4ee7bed65a7bcbe6d7ebbbd0a7f87d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063799"
---
# <a name="spatial-results-window"></a>Ventana Resultados espaciales
  La ventana **Resultados espaciales** proporciona herramientas de asignación visual para ver los datos espaciales. Para ver los resultados espaciales, los resultados de la consulta deben incluir una columna espacial con datos de geometría o de geografía.  
  
> [!NOTE]  
>  La ventana **Resultados espaciales** solo está disponible si los resultados se devuelven a una cuadrícula en la ventana **Resultados** . Si especifica que los resultados se deben devolver como texto, esta ventana no está disponible.  
  
## <a name="options"></a>Opciones  
 **Seleccionar columna espacial**  
 Especifique la columna espacial que desea ver en las columnas espaciales de los resultados de la consulta. Solo puede seleccionarse una columna cada vez.  
  
 **Seleccionar columna de etiqueta**  
 Especifique la columna no espacial en las columnas devueltas en los resultados de la consulta para etiquetar los datos espaciales. Solo puede seleccionarse una columna cada vez.  
  
 Esta opción no está disponible si solo se devuelven instancias de punto en una consulta.  
  
 **Seleccionar proyección**  
 Muestre los datos de geografía en una de estas cuatro proyecciones: Equirectangular, Mercator, Robinson o Bonne.  
  
 Esta opción no está disponible para los datos de geometría.  
  
 **Zoom**  
 Ajuste la presentación del mapa en una escala exponencial.  
  
 **Mostrar líneas de cuadrícula**  
 Activa o desactiva las líneas de cuadrícula de coordenadas.  
  
 En las formas de polígono, la etiqueta solo se muestra cuando la forma es lo suficientemente grande como para contener el texto del rótulo. Si desea mostrar las etiquetas para las formas pequeñas, ajuste el zoom.  
  
> [!NOTE]  
>  Las instancias de punto no se pueden etiquetar.  
  
## <a name="see-also"></a>Vea también  
 [Ver datos espaciales en el Explorador de objetos](view-spatial-data-in-object-explorer.md)   
 [Datos espaciales &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)   
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](query-and-text-editors-sql-server-management-studio.md)  
  
  
