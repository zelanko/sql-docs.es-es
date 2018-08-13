---
title: sp_helpsort (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpsort_TSQL
- sp_helpsort
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsort
ms.assetid: 2a88d079-3755-43cb-8a54-97d0114149e6
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b72de312f8d3ab7abadc592b14149d47f65dfa7a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39539415"
---
# <a name="sphelpsort-transact-sql"></a>sp_helpsort (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra el criterio de ordenación y el juego de caracteres de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsort  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve la intercalación predeterminada del servidor.  
  
## <a name="remarks"></a>Notas  
 Si una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala con una intercalación especificada para que sea compatible con una instalación anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_helpsort** devuelve resultados en blanco. En casos como éste, se puede determinar la intercalación consultando el objeto SERVERPROPERTY; por ejemplo: `SELECT SERVERPROPERTY ('Collation');`.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra el nombre del criterio de ordenación predeterminado del servidor, su juego de caracteres y una tabla con sus principales valores de ordenación.  
  
```  
sp_helpsort;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Server default collation`  
  
 `------------------------`  
  
 `Latin1-General, case-sensitive, accent-sensitive, kanatype-insensitive, width-insensitive for Unicode Data, SQL Server Sort Order 51 on Code Page 1252 for non-Unicode Data.`  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  
