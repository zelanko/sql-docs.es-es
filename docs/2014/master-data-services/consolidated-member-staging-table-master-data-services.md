---
title: Tabla de ensayo de miembros consolidados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b0ade33df500a35f8319a2eb0bc412e16b2d1cf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480041"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>Tabla de ensayo de miembros consolidados (Master Data Services)
  Use la tabla de almacenamiento provisional de miembros consolidados (stg.name_Consolidated) de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para crear, actualizar, desactivar y eliminar miembros consolidados. También puede usarla para actualizar valores de atributos de miembros consolidados.  
  
##  <a name="TableColumns"></a>Columnas de la tabla  
 En la tabla siguiente se explica para qué se usa cada uno de los campos de la tabla de ensayo Consolidated.  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**SESIÓN**|Identificador asignado automáticamente. No especifique ningún valor en este campo. Si no se ha procesado el lote, este campo está en blanco.|  
|**ImportType**<br /><br /> Obligatorio|Determina qué se debe hacer si los datos almacenados provisionalmente coinciden con datos que ya existen en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> **0**: crear nuevos miembros. Reemplazar los datos de MDS existentes con datos almacenados provisionalmente, pero solo si los datos almacenados provisionalmente no son NULL. Los valores NULL se pasan por alto. Para cambiar un valor de atributo a NULL, use **~NULL~**.<br /><br /> **1**: crear solo miembros nuevos. Todas las actualizaciones de datos MDS existentes producen un error.<br /><br /> **2**: crear nuevos miembros. Reemplazar los datos de MDS con datos almacenados provisionalmente. Si importa valores NULL, sobrescribirán los valores de MDS existentes.<br /><br /> **3**: desactivar el miembro, según el valor del código. Se conservan todos los atributos, pertenencias a jerarquías y colecciones, y transacciones pero ya no están disponibles en la interfaz de usuario. Si se utiliza el miembro como valor de atributo basado en dominio de otro miembro, la desactivación producirá un error.<br /><br /> **4**: eliminar definitivamente el miembro, según el valor del código. Todos los atributos, pertenencias a jerarquías y colecciones, y transacciones se eliminan de forma permanente. Si se utiliza el miembro como valor de atributo basado en dominio de otro miembro, la eliminación producirá un error.|  
|**ImportStatus_ID**<br /><br /> Obligatorio|Estado del proceso de importación. Los valores posibles son:<br /><br /> **0**, que se especifica para indicar que el registro está listo para el almacenamiento provisional.<br /><br /> **1**, que se asigna automáticamente e indica que el proceso de almacenamiento provisional del registro se ha realizado correctamente.<br /><br /> **2**, que se asigna automáticamente e indica que se ha producido un error en el proceso de almacenamiento provisional del registro.|  
|**Batch_ID**<br /><br /> Solo lo necesita el servicio web|Identificador asignado automáticamente que agrupa los registros para el almacenamiento provisional. A todos los miembros del lote se les asigna este identificador, que se muestra en la columna [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Id. **de la interfaz de usuario de** .<br /><br /> Si no se ha procesado el lote, este campo está en blanco.|  
|**BatchTag**<br /><br /> Obligatorio, excepto para el servicio web|Nombre único para el lote, de hasta 50 caracteres.|  
|**HierarchyName**<br /><br /> Obligatorio|Nombre de jerarquía explícita. Cada miembro consolidado solo puede pertenecer a una jerarquía.|  
|**ErrorCode**|Muestra un código de error. Para todos los registros con un **ImportStatus_ID** de **2**, consulte [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
|**Código**<br /><br /> Obligatorio, excepto cuando los códigos se generan de forma automática para **ImportType1** o **2**; consulte [Creación automática de código &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md) para obtener más información|Código único del miembro.|  
|**Nombre**<br /><br /> Opcional|Nombre del miembro.|  
|**NewCode**|Úselo solo si va a cambiar el código de miembro.|  
|\<Nombre de atributo>|Existe una columna para cada atributo de la entidad. Úsela con un **ImportType** de **0** o **2**. Para los atributos de forma libre, especifique el nuevo texto o valor de cadena para el atributo. Para los atributos basados en dominio, especifique el código del miembro que será el atributo. Para los atributos de enlace, la dirección URL debe comenzar con **http://**.<br /><br /> Nota: No puede almacenar de forma provisional los atributos de archivo.|  
  
## <a name="see-also"></a>Consulte también  
 [Cargar o actualizar miembros en Master Data Services mediante el proceso de almacenamiento provisional](add-update-and-delete-data-master-data-services.md)   
 [Mueva los miembros de la jerarquía explícita mediante el proceso de almacenamiento provisional &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Master Data Services de &#40;de importación de datos&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Ver los errores que se producen durante el proceso de almacenamiento provisional &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
