---
title: Sys.numbered_procedure_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- numbered_procedure_parameters_TSQL
- sys.numbered_procedure_parameters_TSQL
- numbered_procedure_parameters
- sys.numbered_procedure_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedure_parameters catalog view
ms.assetid: a441d46d-1f30-41c2-8d94-e9442f59786e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0594feab6b69a9917b084cfa20c71af9885a880a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021902"
---
# <a name="sysnumberedprocedureparameters-transact-sql"></a>sys.numbered_procedure_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada parámetro de un procedimiento numerado. Cuando se crea un procedimiento almacenado numerado, el procedimiento base es el número 1. Todos los procedimientos subsiguientes tienen los números 2, 3, etc. **Sys.numbered_procedure_parameters** contiene las definiciones de parámetro para todos los procedimientos siguientes, numerados de 2 y versiones posteriores. Esta vista no muestra los parámetros del procedimiento almacenado base (número = 1). El procedimiento almacenado base es similar a un procedimiento almacenado no numerado. Por lo tanto, sus parámetros se representan en [sys.parameters (Transact-SQL)](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md).  
  
> [!IMPORTANT]  
>  Los procedimientos numerados son desusados. Por tanto, se desaconseja su uso. Se desencadena un evento DEPRECATION_ANNOUNCEMENT cuando se compila una consulta que utiliza esta vista de catálogo.  
  
> [!NOTE]  
>  Los parámetros XML y CLR no son compatibles con los procedimientos numerados.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece el parámetro.|  
|**procedure_number**|**smallint**|Número de este procedimiento en el objeto, 2 o mayor.|  
|**Nombre**|**sysname**|Nombre del parámetro. Es único dentro de **procedure_number**.|  
|**parameter_id**|**int**|Id. del parámetro. Es único dentro de la **procedure_number**.|  
|**system_type_id**|**tinyint**|Id. del tipo de sistema del parámetro.|  
|**user_type_id**|**int**|Id. del tipo, definido por el usuario, del parámetro.|  
|**max_length**|**smallint**|Longitud máxima del parámetro en bytes.<br /><br /> -1 = El tipo de datos de las columnas es varchar(max), nvarchar(max) o varbinary(max).|  
|**Precisión**|**tinyint**|Precisión del parámetro si está basado en numerales; de lo contrario es 0.|  
|**Escala**|**tinyint**|Escala del parámetro si está basado en numerales; de lo contrario es 0.|  
|**is_output**|**bit**|1 = El parámetro es de salida o retorno; de lo contrario, es 0|  
|**is_cursor_ref**|**bit**|1 = El parámetro es un parámetro de referencia a un cursor.|  
  
> [!NOTE]  
>  Los parámetros XML y CLR no son compatibles con los procedimientos numerados.  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
