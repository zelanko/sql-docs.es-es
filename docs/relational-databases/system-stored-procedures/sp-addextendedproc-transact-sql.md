---
title: sp_addextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc8ea22699762927a026ae4cc811500c193555c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072752"
---
# <a name="spaddextendedproc-transact-sql"></a>sp_addextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra el nombre de un nuevo procedimiento almacenado extendido a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, use la [integración con CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @functname = ] 'procedure'` Es el nombre de la función para llamar a dentro de la biblioteca de vínculos dinámicos (DLL). *procedimiento* es **nvarchar (517)** , no tiene ningún valor predeterminado. *procedimiento* puede incluir opcionalmente el nombre del propietario en el formulario *owner.function*.  
  
`[ @dllname = ] 'dll'` Es el nombre del archivo DLL que contiene la función. *DLL* es **varchar (255)** , no tiene ningún valor predeterminado. Se recomienda especificar la ruta de acceso completa del archivo DLL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Después de crea un procedimiento almacenado extendido, debe agregarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando **sp_addextendedproc**. Para obtener más información, consulte [agregar un procedimiento almacenado extendido a SQL Server](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md).  
  
 Este procedimiento se puede ejecutar solo en el **maestro** base de datos. Para ejecutar un procedimiento almacenado extendido desde una base de datos distinto **maestro**, califique el nombre del procedimiento almacenado extendido con **maestro**.  
  
 **sp_addextendedproc** agrega entradas a la [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista de catálogo, registrar el nombre del nuevo procedimiento almacenado extendido con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También agrega una entrada en el [sys.extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) vista de catálogo.  
  
> [!IMPORTANT]  
>  Las DLL existentes que no se registraron con una ruta completa no funcionarán tras una actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para corregir el problema, utilice **sp_dropextendedproc** para anular el registro de la DLL y, a continuación, vuelva a registrarlo con **sp_addextendedproc**, especificando la ruta completa.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_addextendedproc**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega el **xp_hello** el procedimiento almacenado extendido.  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>Vea también  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
