---
title: Ventana Resultados espaciales | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2d5a477-6496-4d01-adee-7322ebdfadf3
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8a10eaf4ad3104f6fd9aee961ae669711940e2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spatial-results-window"></a>Ventana Resultados espaciales
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] La ventana **Resultados espaciales** proporciona herramientas de asignación visual para ver los datos espaciales. Para ver los resultados espaciales, los resultados de la consulta deben incluir una columna espacial con datos de geometría o de geografía.  
  
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
 [Ver datos espaciales en el Explorador de objetos](../../relational-databases/scripting/view-spatial-data-in-object-explorer.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Editor de consultas del motor de base de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
