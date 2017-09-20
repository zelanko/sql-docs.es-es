---
title: Combinar datos (Complemento MDS para Excel) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 8a8ee3e56e5b8ed42bca6b30192c3b14686d1240
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="combine-data-mds-add-in-for-excel"></a>Combinar datos (Complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], combine los datos de dos hojas de cálculo si desea comparar los datos antes de publicarlos. En este procedimiento, se combinan los datos de dos hojas de cálculo en una. Puede realizar otras comparaciones y determinar qué datos publicar en el repositorio MDS.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe tener una hoja de cálculo activa que contenga los datos administrados por MDS. Para obtener más información, consulte [Exportar datos a Excel desde Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
-   Debe tener una hoja de cálculo que contenga los datos que desea combinar con los datos administrados por MDS. Esta hoja debe tener una fila de encabezado.  
  
### <a name="to-combine-non-managed-data-into-an-mds-managed-sheet"></a>Para combinar los datos no administrados en una hoja administrada por MDS  
  
1.  En la hoja que contiene los datos administrados por MDS, en el grupo **Publicar y validar** , haga clic en **Combinar datos**.  
  
2.  En el cuadro de diálogo **Combinar datos** , junto al cuadro de texto **Intervalo para combinar con los datos MDS** , haga clic en el icono. El cuadro de diálogo se contrae.  
  
3.  Haga clic en la hoja que contiene los datos que desea combinar.  
  
4.  Resalte todas las celdas de la hoja que desea combinar, incluida la fila de encabezado.  
  
5.  En el cuadro de diálogo **Combinar datos** , haga clic en el icono. El cuadro de diálogo se expande.  
  
6.  Para una columna enumerada para la entidad MDS, seleccione una columna debajo de **Columna correspondiente**. Ninguna columna MDS necesita las columnas correspondientes.  
  
7.  Haga clic en **Combinar**. Se muestra una columna **SOURCE** , que indica si los datos son de MDS o un origen externo.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   Para buscar similitudes entre los datos administrados por MDS y los datos externos, vea [Coincidir datos similares &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general: Exportar datos a Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Coincidencia de calidad de datos en el Complemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  
