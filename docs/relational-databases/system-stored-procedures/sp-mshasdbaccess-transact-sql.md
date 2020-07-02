---
title: sp_MShasdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_MShasdbaccess
- sp_MShasdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_MShasdbaccess
ms.assetid: a9a23b90-2c60-4460-80a7-d7e14cc5a6a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 835a62edd78dec85bb1d05fe40dfddbbf819bc6f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757857"
---
# <a name="sp_mshasdbaccess-transact-sql"></a>sp_MShasdbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Muestra una lista con el nombre y el propietario de todas las bases de datos a las que tiene acceso el usuario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_MShasdbaccess      
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Se concede el permiso Execute al rol **Public** .  
  
## <a name="see-also"></a>Consulte también  
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)  
  
  
