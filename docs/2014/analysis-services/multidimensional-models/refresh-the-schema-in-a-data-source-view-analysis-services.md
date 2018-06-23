---
title: Actualizar el esquema de una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data source views [Analysis Services], schema updates
- refreshing data source views
- data source views [Analysis Services], refreshing
ms.assetid: 634b0504-1437-43e7-8ac7-3248ac7989a3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 517c3e9c0c608a0e38d79fd6aff8147a68403671
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112798"
---
# <a name="refresh-the-schema-in-a-data-source-view-analysis-services"></a>Actualizar el esquema de una vista del origen de datos (Analysis Services)
  Después de definir una vista del origen de datos (DSV) en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], el esquema de un origen de datos subyacente puede cambiar. Estos cambios no se detectan ni se actualizan automáticamente en un proyecto de desarrollo. Además, si implementó el proyecto en un servidor y Analysis Services no puede establecer conexión con el origen de datos externo, se producirán errores de procesamiento.  
  
 Para actualizar la DSV de forma que coincida con el origen de datos externo, puede hacerlo en Business Intelligence Development Studio (BIDS). El proceso de actualización de la DSV detecta los cambios que se han producido en los orígenes de datos externos en los que se basa la DSV, y crea una lista con dichos cambios; en ella se enumeran las adiciones o eliminaciones que han tenido lugar en el origen de datos externo. A continuación, puede aplicar el conjunto de cambios a la DSV para que esta se vuelva a alinear con el origen de datos subyacente. Tenga en cuenta que a menudo es necesario trabajo adicional para actualizar los cubos y las dimensiones del proyecto que usa la DSV.  
  
 En este tema se incluyen las secciones siguientes:  
  
 [Cambios admitidos en la actualización](#bkmk_changlist)  
  
 [Actualizar una DSV en SQL Server Data Tools](#bkmk_DSVrefresh)  
  
##  <a name="bkmk_changlist"></a> Cambios admitidos en la actualización  
 La actualización de la DSV puede incluir cualquiera de las acciones siguientes:  
  
-   Eliminación de tablas, columnas y relaciones  
  
-   Adición de columnas y relaciones, aplicadas a las tablas que ya están incluidas en la DSV  
  
-   Adición de nuevas restricciones únicas. Si existe una clave principal lógica para una tabla en la DSV y se agrega una clave física a la tabla del origen de datos, la clave lógica se quita y se reemplaza por la clave física.  
  
 El proceso de actualización nunca agrega nuevas tablas a la DSV. Si desea agregar una nueva tabla, debe hacerlo manualmente. Para obtener más información, vea [Agregar o quitar tablas o vistas en una vista del origen de datos &#40;Analysis Services&#41;](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_DSVrefresh"></a> Actualizar una DSV en SQL Server Data Tools  
 Para actualizar una DSV, haga doble clic en ella desde el Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y, después, haga clic en el botón Actualizar vista del origen de datos o elija **Actualizar** en el menú Vista del origen de datos.  
  
 Durante la actualización, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] consulta todos los orígenes de datos relacionales subyacentes para determinar si ha habido cambios en las tablas o en las vistas incluidas en la DSV. Si se pueden establecer conexiones con todos los orígenes de datos subyacentes y se han producido cambios, los verá en el cuadro de diálogo **Actualizar vista del origen de datos** .  
  
 ![Actualizar el cuadro de diálogo de vista del origen de datos](../media/ssas-olapdsv-refresh.gif "cuadro de diálogo Actualizar vista del origen de datos")  
  
 El cuadro de diálogo muestra las tablas, columnas, restricciones y relaciones que se eliminarán o agregarán en la DSV. El informe también muestra cualquier cálculo o consulta con nombre que no se haya preparado correctamente. Los objetos afectados se muestran en una vista de árbol con columnas y relaciones anidadas bajo tablas y el tipo de cambio (eliminación o adición) indicado para cada objeto. Los iconos de objeto de vista del origen de datos estándar indican el tipo de objeto afectado.  
  
 La actualización se basa completamente en los nombres de los objetos subyacentes. Por lo tanto, si se cambia el nombre a un objeto subyacente en el origen de datos, el Diseñador de vistas del origen de datos trata el objeto con el nombre cambiado como dos operaciones independientes: una eliminación y una adición. En este caso, es posible que deba volver a agregar manualmente el objeto con el nombre cambiado a la vista del origen de datos. También es posible que tenga que volver a crear relaciones o claves principales lógicas.  
  
> [!IMPORTANT]  
>  Si es consciente de que ha cambiado el nombre a una tabla de un origen de datos, es posible que desee usar el comando **Reemplazar tabla** para reemplazar la tabla por la tabla con el nuevo nombre antes de actualizar la vista del origen de datos. Para obtener más información, vea [Reemplazar una tabla o una consulta con nombre en una vista del origen de datos &#40;Analysis Services&#41;](replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md).  
  
 Después de examinar el informe, puede aceptar los cambios o cancelar la actualización para rechazarlos. Todos los cambios se deben aceptar o rechazar en conjunto. No puede elegir elementos individuales de la lista. También puede guardar un informe de los cambios.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)  
  
  