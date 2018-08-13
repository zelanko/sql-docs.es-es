---
title: Sys.Schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 332974efa3de965a369ca66b567b36ac254e19f7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39558755"
---
# <a name="schemas-catalog-views---sysschemas"></a>-Las vistas de catálogo de esquemas sys.schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una fila por cada esquema de la base de datos.  
  
> [!NOTE]  
>  Los esquemas de la base de datos son diferentes de los esquemas XML, que se utilizan para definir el modelo de contenido de los documentos XML.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del esquema. Es único en la base de datos.|  
|**schema_id**|**int**|Id. del esquema. Es único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad propietaria del esquema.|  
  
## <a name="remarks"></a>Notas  
 Esquemas de base de datos actúan como espacios de nombres o contenedores de objetos, como tablas, vistas, procedimientos y funciones, que pueden encontrarse en el **sys.objects** vista de catálogo.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de esquemas &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
