---
title: Columnas de coincidencia de calidad de datos (Complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 939ec9727cc81ce3b206b8bc7ca3ed8dd62c3877
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961305"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Columnas de coincidencia de calidad de datos (Complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], después de buscar los datos coincidentes, en el grupo **Calidad de datos** en la cinta de opciones, puede hacer clic en **Mostrar detalles** para ver las columnas que proporcionan detalles de la coincidencia.  
  
 La tabla siguiente se muestra las columnas que se presentan al coincidir los datos.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**CLUSTER_ID**|Identificador único que se usa para agrupar registros similares. Todas las filas similares tienen el mismo **CLUSTER_ID**. Si no se muestra ningún **CLUSTER_ID** para una fila, es porque no se han encontrado registros similares.|  
|**RECORD_ID**|Identificador único que se usa para identificar los registros. Similar al valor del código almacenado en el repositorio MDS, es un valor que se usa para identificar un registro. Se genera automáticamente cada vez que se realiza la coincidencia.|  
|**PIVOT_MARK**|Registro arbitrario con el que otros registros se comparan; no tiene un valor de puntuación.|  
|**CARÁCTER**|Representa el grado de similitud de los registros del grupo con el registro dinámico. Esta puntuación está determinada por DQS. Si no se muestra ninguna puntuación, el registro es la dinamización para otros registros o no se encontraron coincidencias.|  
  
## <a name="see-also"></a>Consulte también  
 [Coincidencia de calidad de datos en el Complemento MDS para Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Coincide con &#40;de datos similares Complemento MDS para Excel&#41;](match-similar-data-mds-add-in-for-excel.md)   
 [Coincidencia de datos](../../data-quality-services/data-matching.md)  
  
  
