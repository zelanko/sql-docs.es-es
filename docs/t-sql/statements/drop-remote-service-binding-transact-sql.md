---
title: DROP REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP REMOTE SERVICE BINDING
- DROP_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping remote service bindings
- removing remote service bindings
- deleting remote service bindings
- remote service bindings [Service Broker], dropping
- DROP REMOTE SERVICE BINDING statement
ms.assetid: 377789b4-bf94-488f-8c20-687d0bae447a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 54890859e9ec27ebfb91009632245d4807f6897a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68044045"
---
# <a name="drop-remote-service-binding-transact-sql"></a>DROP REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un enlace de servicio remoto.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP REMOTE SERVICE BINDING binding_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 Es el nombre del enlace de servicio remoto que se va a quitar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, el permiso para quitar un enlace de servicio remoto corresponde al propietario del enlace de servicio remoto, a los miembros del rol fijo de base de datos db_owner y a los miembros del rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina el enlace de servicio remoto `APBinding` de la base de datos.  
  
```  
DROP REMOTE SERVICE BINDING APBinding ;  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
