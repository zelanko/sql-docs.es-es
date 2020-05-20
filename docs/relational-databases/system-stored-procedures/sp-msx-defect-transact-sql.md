---
title: sp_msx_defect (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1bc6139afdf99fad7a6abcf5134e3341e7a8082c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828823"
---
# <a name="sp_msx_defect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el servidor actual de las operaciones multiservidor.  
  
> [!CAUTION]  
>  **sp_msx_defect** edita el registro. No se recomienda la modificación manual del Registro porque los cambios inapropiados o incorrectos pueden causar graves problemas de configuración en el sistema. Por tanto, solo los usuarios experimentados deben utilizar el programa Editor del Registro para modificar el Registro. Para obtener más información, consulte la documentación de Microsoft Windows.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @forced_defection = ] forced_defection`Especifica si se debe forzar la baja o no si se ha perdido permanentemente el SQLServerAgent maestro debido a una base de datos **msdb** dañada irreversible o a ninguna copia de seguridad de base de datos **msdb** . *forced_defection*es de **bit**y su valor predeterminado es **0**, que indica que no se debe producir ninguna baja forzada. Un valor de **1** fuerza la baja.  
  
 Después de forzar una baja ejecutando **sp_msx_defect**, un miembro del rol fijo de servidor **sysadmin** en el SQLServerAgent maestro debe ejecutar el siguiente comando para completar la baja:  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 Cuando **sp_msx_defect** se completa correctamente, se devuelve un mensaje.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="see-also"></a>Consulte también  
 [sp_msx_enlist &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
