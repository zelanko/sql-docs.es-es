---
title: sp_enumdsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f58a16b3d4d393a94dc5e42413ddfeb2a8eb5d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62520941"
---
# <a name="spenumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de todos los nombres de orígenes de datos ODBC y OLE DB definidos de un servidor que se ejecuta en una cuenta de usuario específica de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre del origen de datos**|**sysname**|Nombre del origen de datos.|  
|**Descripción**|**varchar(255)**|Descripción del origen de datos.|  
|**Tipo**|**int**|Tipo del origen de datos.<br /><br /> **1** = ODBC DSN<br /><br /> **3** = origen de datos OLE DB|  
|**Nombre del proveedor**|**varchar(255)**|Nombre del proveedor OLE DB. El valor es NULL para DSN de ODBC.|  
  
## <a name="remarks"></a>Comentarios  
 Cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio tiene un contexto de usuario. Un contexto de usuario es un conjunto de entradas del Registro que incluye las definiciones de los orígenes de datos ODBC del usuario. El nombre de usuario con el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el contexto de usuario.  
  
 Por ejemplo, si el servidor se está ejecutando en el contexto de usuario de la cuenta del sistema, todos los nombres de origen de datos (DSN) obtenidos serán DSN del sistema asociados a la cuenta de sistema. Si el servidor se ejecuta con una cuenta de usuario privada, solo se devolverán los DSN definidos para esa cuenta.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_enumdsn**.  
  
## <a name="see-also"></a>Vea también  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
