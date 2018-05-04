---
title: sp_msx_enlist (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_msx_enlist_TSQL
- sp_msx_enlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_enlist
ms.assetid: ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 29dc5e5d485b16e8d7550e607440541b13bd5e23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spmsxenlist-transact-sql"></a>sp_msx_enlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega el servidor actual a la lista de servidores disponibles en el servidor maestro.  
  
> [!CAUTION]  
>  El **sp_msx_enlist** procedimiento almacenado modifica el registro. No se recomienda la modificación manual del Registro porque los cambios inapropiados o incorrectos pueden causar graves problemas de configuración en el sistema. Por tanto, solo los usuarios experimentados deben utilizar el programa Editor del Registro para modificar el Registro. Para obtener más información, consulte la documentación de Microsoft Windows.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_msx_enlist [@msx_server_name =] 'msx_server'   
     [, [@location =] 'location']  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@msx_server_name =**] **'***msx_server***'**  
 Nombre del servidor de administración multiservidor (maestro). *msx_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@location =**] **'***ubicación***'**  
 Ubicación del servidor de destino que se va a agregar. *ubicación* es **nvarchar (100)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissions  
 Los permisos de ejecución para este procedimiento corresponden de forma predeterminada a los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo dar de alta el servidor actual en el servidor maestro `AdventureWorks1`. La ubicación del servidor actual es `Building 21, Room 309, Rack 5`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [xp_cmdshell &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)  
  
  
