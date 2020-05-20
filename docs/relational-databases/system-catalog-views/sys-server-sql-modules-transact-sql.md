---
title: Sys. server_sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bd4eba56c6550f4a3ae8b033dbd81b71ac7b5418
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821431"
---
# <a name="sysserver_sql_modules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene el conjunto de módulos SQL para los desencadenadores de nivel de servidor de tipo TR. Puede combinar esta relación con sys.server_triggers. La tupla (object_id) es la clave de la relación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Se trata de una referencia FOREIGN KEY al desencadenador de nivel de servidor en el que se define este módulo.|  
|**definir**|**nvarchar(max)**|Texto SQL que define este módulo.<br /><br /> NULL = Cifrado.|  
|**uses_ansi_nulls**|**bit**|El módulo fue creado con la opción de conjunto ANSI NULLS establecida en ON.|  
|**uses_quoted_identifier**|**bit**|El módulo fue creado con la opción de conjunto QUOTED IDENTIFIER establecida en ON.|  
|**execute_as_principal_id**|**int**|Id. de la entidad de seguridad de servidor EXECUTE AS.<br /><br /> NULL de manera predeterminada o si EXECUTE AS CALLER <br /><br /> IDENTIFICADOR de la entidad de seguridad especificada si EXECUTe AS SELF EXECUTe as principal-2 = EXECUTe AS OWNER.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
