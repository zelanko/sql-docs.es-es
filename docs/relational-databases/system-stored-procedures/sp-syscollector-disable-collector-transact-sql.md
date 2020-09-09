---
description: sp_syscollector_disable_collector (Transact-SQL)
title: sp_syscollector_disable_collector (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_disable_collector_TSQL
- sp_syscollector_disable_collector
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_disable_collector
ms.assetid: 9ef4c85d-cca6-452d-94be-2be6f616c3d8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3453a78c8d5edde0db4e087af4bc2501e3b4232a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549534"
---
# <a name="sp_syscollector_disable_collector-transact-sql"></a>sp_syscollector_disable_collector (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Deshabilita el recopilador de datos. Dado que solamente hay un recopilador de datos por servidor, no se requiere ningún parámetro.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dbo.sp_syscollector_disable_collector   
```  
  
## <a name="arguments"></a>Argumentos  
 Ninguno  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 Tiene como valor predeterminado el recopilador de datos en el servidor.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos **dc_admin** o **dc_operator** (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se deshabilita el recopilador de datos.  
  
```  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
