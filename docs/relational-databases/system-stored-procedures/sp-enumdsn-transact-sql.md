---
title: sp_enumdsn (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e8d4dcb23cf06385d4c26a198f17e806bdc0671a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
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
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre del origen de datos**|**sysname**|Nombre del origen de datos.|  
|**Description**|**varchar (255)**|Descripción del origen de datos.|  
|**Tipo**|**int**|Tipo del origen de datos.<br /><br /> **1** = DSN DE ODBC<br /><br /> **3** = origen de datos OLE DB|  
|**Nombre del proveedor**|**varchar (255)**|Nombre del proveedor OLE DB. El valor es NULL para DSN de ODBC.|  
  
## <a name="remarks"></a>Comentarios  
 Cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio tiene un contexto de usuario. Un contexto de usuario es un conjunto de entradas del Registro que incluye las definiciones de los orígenes de datos ODBC del usuario. El nombre de usuario con el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el contexto de usuario.  
  
 Por ejemplo, si el servidor se está ejecutando en el contexto de usuario de la cuenta del sistema, todos los nombres de origen de datos (DSN) obtenidos serán DSN del sistema asociados a la cuenta de sistema. Si el servidor se ejecuta con una cuenta de usuario privada, solo se devolverán los DSN definidos para esa cuenta.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_enumdsn**.  
  
## <a name="see-also"></a>Vea también  
 [sp_dsninfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
