---
title: Sys.Triggers (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33eb5a1c4176041d64ba60a3a684b75bc4816350
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091927"
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada objeto que es un desencadenador, con un tipo TR o TA. Nombres de los desencadenadores DML tienen el ámbito de esquema y, por lo tanto, están visibles en **sys.objects**. Los nombres de desencadenador DDL se incluyen en el ámbito mediante la entidad primaria y solo se pueden ver en esta vista.  
  
 El **parent_class** y **nombre** columnas identifican de forma única el desencadenador en la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del desencadenador. Los nombres de desencadenador DML se encuentran en el ámbito de esquema. Los nombres de desencadenador DDL se encuentran en el ámbito con respecto a la entidad primaria.|  
|**object_id**|**int**|Número de identificación del objeto. Es único en una base de datos.|  
|**parent_class**|**tinyint**|Clase del elemento primario del desencadenador.<br /><br /> 0 = Base de datos para los desencadenadores DDL.<br /><br /> 1 = Objeto o columna para los desencadenadores DML.|  
|**parent_class_desc**|**nvarchar(60)**|Descripción de la clase primaria del desencadenador.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|Id. del elemento primario del desencadenador, como se indica a continuación:<br /><br /> 0 = Desencadenadores que son desencadenadores primarios de la base de datos.<br /><br /> Los desencadenadores DML, se trata la **object_id** de la tabla o vista en el que está definido el desencadenador DML.|  
|**type**|**char(2)**|Tipo de objeto:<br /><br /> TA = Desencadenador de ensamblado (CLR)<br /><br /> TR = Desencadenador SQL|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de objeto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|Fecha de creación del desencadenador.|  
|**modify_date**|**datetime**|Fecha en que se modificó el objeto por última vez con una instrucción ALTER.|  
|**is_ms_shipped**|**bit**|Desencadenador creado en nombre del usuario por un componente interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|Se ha deshabilitado el desencadenador.|  
|**is_not_for_replication**|**bit**|Se ha creado el desencadenador como NOT FOR REPLICATION.|  
|**is_instead_of_trigger**|**bit**|1 = Desencadenadores INSTEAD OF<br /><br /> 0 = Desencadenadores AFTER|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
