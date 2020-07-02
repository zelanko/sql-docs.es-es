---
title: sp_OADestroy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 94dcbd7a3b2933d41994bbefda40aff755e978a3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645923"
---
# <a name="sp_oadestroy-transact-sql"></a>sp_OADestroy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Destruye un objeto OLE creado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 Es el token de objeto de un objeto OLE creado previamente mediante **sp_OACreate**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un valor distinto de cero (error) que es el valor entero del HRESULT devuelto por el objeto de OLE Automation.  
  
 Para obtener más información sobre los códigos de retorno de HRESULT, vea [códigos de retorno e información de error de automatización OLE](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Comentarios  
 Si no se llama a **sp_OADestroy** , el objeto OLE creado se destruye automáticamente al final del lote.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** o al permiso Execute directamente en este procedimiento almacenado. `Ole Automation Procedures`la configuración debe estar **habilitada** para usar cualquier procedimiento del sistema relacionado con la automatización OLE.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se destruye el objeto **SQLServer** creado previamente.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de automatización OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Ejemplo de script de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
