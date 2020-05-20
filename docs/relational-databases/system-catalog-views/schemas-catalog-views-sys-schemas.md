---
title: Sys. Schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2f4aa79f2c93e1c78c895f0e3d47e3114df20a8c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834470"
---
# <a name="schemas-catalog-views---sysschemas"></a>Vistas de catálogo de esquemas: sys. Schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una fila por cada esquema de la base de datos.  
  
> [!NOTE]  
>  Los esquemas de la base de datos son diferentes de los esquemas XML, que se utilizan para definir el modelo de contenido de los documentos XML.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del esquema. Es único en la base de datos.|  
|**schema_id**|**int**|Id. del esquema. Es único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad propietaria del esquema.|  
  
## <a name="remarks"></a>Observaciones  
Los esquemas de base de datos actúan como espacios de nombres o contenedores para objetos, como tablas, vistas, procedimientos y funciones, que se pueden encontrar en la vista de catálogo **Sys. Objects** .  

Cada esquema tiene un propietario. El propietario es una [entidad](../../relational-databases/security/authentication-access/principals-database-engine.md)de seguridad.
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
[Principals](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Vistas de catálogo de esquemas &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
