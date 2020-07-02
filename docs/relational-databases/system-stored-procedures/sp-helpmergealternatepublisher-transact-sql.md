---
title: sp_helpmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords:
- sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd1071dd1ca4e2951dc3a7d1fbc759ae13b968f6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733141"
---
# <a name="sp_helpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una lista de todos los servidores habilitados como publicadores alternativos para publicaciones de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador alternativo. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|Nombre del publicador alternativo.|  
|**alternate_publisher_db**|**sysname**|Nombre de la base de datos de publicaciones.|  
|**alternate_publication**|**sysname**|Nombre de la publicación.|  
|**alternate_distributor**|**sysname**|Nombre del distribuidor.|  
|**friendly_name**|**nvarchar(255)**|Descripción del publicador alternativo.|  
|**activó**|**bit**|Especifica si el servidor es un publicador alternativo. **1** especifica que el publicador está habilitado como publicador alternativo. **0** especifica que no está habilitado.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergealternatepublisher** se utiliza en la replicación de mezcla.  
  
 Durante cada sesión de mezcla, el sistema consulta tanto al publicador como al suscriptor para obtener la lista de publicadores alternativos de cada uno. El proceso de mezcla agrega entradas a la lista de publicadores alternativos o las quita. El resultado es que las listas de publicadores alternativos del suscriptor y el publicador coinciden.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la lista de acceso a la publicación pueden ejecutar **sp_helpmergealternatepublisher**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
