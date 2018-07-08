---
title: Tabla de ensayo de relaciones (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 38b92d05a119af10a3c6c2e464b745b8fb26b197
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229335"
---
# <a name="relationship-staging-table-master-data-services"></a>Tabla de ensayo de relaciones (Master Data Services)
  Use la tabla de almacenamiento provisional de relaciones (stg.name_Relationship) en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para cambiar la ubicación de los miembros de una jerarquía explícita, en función de las relaciones que tienen los miembros entre sí.  
  
##  <a name="TableColumns"></a> Columnas de la tabla  
 En la tabla siguiente se explica para qué se usa cada uno de los campos de la tabla de ensayo Relationship.  
  
|Nombre de la columna|Descripción|  
|-----------------|-----------------|  
|**ID**|Identificador asignado automáticamente. No especifique ningún valor en este campo. Si no se ha procesado el lote, este campo está en blanco.|  
|**RelationshipType**<br /><br /> Obligatorio|Tipo de relación que se está estableciendo. Los valores posibles son:<br /><br /> **1**: primario<br /><br /> **2**: relacionado (del mismo nivel)|  
|**ImportStatus_ID**<br /><br /> Obligatorio|Estado del proceso de importación. Los valores posibles son:<br /><br /> **0**, que se especifica para indicar que el registro está listo para el almacenamiento provisional.<br /><br /> **1**, que se asigna e indica automáticamente que el proceso de almacenamiento provisional del registro ha sido correcto.<br /><br /> **2**, que se asigna automáticamente e indica que el proceso de almacenamiento provisional del registro no ha sido correcto.|  
|**Batch_ID**<br /><br /> Solo lo necesita el servicio web|Identificador asignado automáticamente que agrupa los registros para el almacenamiento provisional. A todos los miembros del lote se les asigna este identificador, que se muestra en la columna [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Id. **de la interfaz de usuario de** .<br /><br /> Si no se ha procesado el lote, este campo está en blanco.|  
|**BatchTag**<br /><br /> Obligatorio, excepto para el servicio web|Nombre único para el lote, de hasta 50 caracteres.|  
|**HierarchyName**<br /><br /> Obligatorio|Nombre de jerarquía explícita. Cada miembro consolidado solo puede pertenecer a una jerarquía.|  
|**ParentCode**<br /><br /> Obligatorio|Para las relaciones de elementos primarios y secundarios, el código del miembro consolidado que será el elemento primario del miembro secundario hoja o consolidado.<br /><br /> Para las relaciones relacionadas, el código de uno de los miembros relacionados.|  
|**ChildCode**<br /><br /> Obligatorio|Para las relaciones de elementos primarios y secundarios, el código del miembro consolidado u hoja que será el elemento secundario.<br /><br /> Para las relaciones relacionadas, el código de uno de los miembros relacionados.|  
|**Criterio de ordenación**<br /><br /> Opcional|Entero que indica el orden del miembro en relación con los demás miembros bajo el elemento primario. Cada miembro secundario debe tener un identificador único.|  
|**ErrorCode**|Muestra un código de error. Para todos los registros con un **ImportStatus_ID** de **2**, consulte [Staging Process Errors &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
  
## <a name="see-also"></a>Vea también  
 [Mover miembros de jerarquías explícitas usando el proceso de almacenamiento provisional &#40;Master Data Services&#41;](/sql/2014/master-data-services/add-update-and-delete-data-master-data-services)   
 [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Ver los errores que se producen durante el proceso de almacenamiento provisional &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Errores del proceso de ensayo &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
