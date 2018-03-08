---
title: Columnas de coincidencia de calidad de datos (Complemento MDS para Excel) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a09a0bcf2136a01545450932623df419c9726250
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Columnas de coincidencia de calidad de datos (Complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], después de buscar los datos coincidentes, en el grupo **Calidad de datos** en la cinta de opciones, puede hacer clic en **Mostrar detalles** para ver las columnas que proporcionan detalles de la coincidencia.  
  
 La tabla siguiente se muestra las columnas que se presentan al coincidir los datos.  
  
|Nombre|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|Identificador único que se usa para agrupar registros similares. Todas las filas similares tienen el mismo **CLUSTER_ID**. Si no se muestra ningún **CLUSTER_ID** para una fila, es porque no se han encontrado registros similares.|  
|**RECORD_ID**|Identificador único que se usa para identificar los registros. Similar al valor del código almacenado en el repositorio MDS, es un valor que se usa para identificar un registro. Se genera automáticamente cada vez que se realiza la coincidencia.|  
|**PIVOT_MARK**|Registro arbitrario con el que otros registros se comparan; no tiene un valor de puntuación.|  
|**SCORE**|Representa el grado de similitud de los registros del grupo con el registro dinámico. Esta puntuación está determinada por DQS. Si no se muestra ninguna puntuación, el registro es la dinamización para otros registros o no se encontraron coincidencias.|  
  
## <a name="see-also"></a>Ver también  
 [Coincidencia de calidad de datos en el Complemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Coincidir datos similares &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Coincidencia de datos](../../data-quality-services/data-matching.md)  
  
  
