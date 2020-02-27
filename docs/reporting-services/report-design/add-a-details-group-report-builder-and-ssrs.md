---
title: Adición de un grupo de detalles (Generador de informes) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5ef8efba-6d48-4aeb-a3b9-a02ba5a44614
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 317b8d31e84078be586fb15986707f39273382d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080766"
---
# <a name="add-a-details-group-report-builder-and-ssrs"></a>Agregar un grupo de detalles (Generador de informes y SSRS)
En un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , los datos detallados de un conjunto de datos de informe se especifican como un grupo sin expresión de grupo. Agregue un grupo de detalles a una región de datos Tablix existente si desea mostrar los datos detallados para una matriz, volver a incluir datos detallados que ha eliminado de una tabla o lista, o agregar grupos de detalles adicionales. Para obtener más información sobre los grupos, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Para agregar un grupo de detalles a una región de datos Tablix  
  
1.  En la superficie de diseño, haga clic en cualquier lugar de una región de datos Tablix para seleccionarla. El panel Agrupación muestra los grupos de filas y de columnas para la región de datos seleccionada.  
  
2.  En el panel Agrupación, haga clic con el botón secundario en un grupo que sea el grupo secundario más interior. Haga clic en **Agregar grupo**y, a continuación, haga clic en **Grupo secundario**. Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
3.  En **Expresión de grupo**, deje en blanco la expresión. Los grupos de detalles no tienen ninguna expresión.  
  
4.  Seleccione **Mostrar datos detallados**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se agrega un nuevo grupo de detalles como un grupo secundario en el panel Agrupación, y el identificador de fila para el grupo seleccionado en el paso 1 muestra el icono de grupo de detalles. Para obtener más información sobre los identificadores, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) [Matrices &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
