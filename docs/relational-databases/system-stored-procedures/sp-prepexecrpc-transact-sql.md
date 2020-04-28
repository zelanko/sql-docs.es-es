---
title: sp_prepexecrpc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fea210183ae67179dcc6f686e25f939cd00713b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056335"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Prepara y ejecuta una llamada a un procedimiento almacenado con parámetros que se ha especificado mediante un identificador de RPC. la sp_prepexecrpc se invoca mediante el identificador 14 en un paquete de flujo TDS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *asa*  
 Es el identificador del controlador preparado generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Handle* es un parámetro necesario con un valor devuelto **int** .  
  
 *RPCCall*  
 Define la llamada a procedimiento almacenado mediante sintaxis canónica de ODBC. *RPCCall* es un parámetro necesario que requiere un valor de entrada de cadena **ntext** .  
  
 *bound_param*  
 Indica el uso opcional de parámetros adicionales. *bound_param* llama a un valor de entrada de cualquier tipo de datos para designar los parámetros adicionales que se usan.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
