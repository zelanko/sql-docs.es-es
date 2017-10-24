---
title: SET FIPS_FLAGGER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FIPS_FLAGGER
- SET_FIPS_FLAGGER_TSQL
- FIPS_FLAGGER_TSQL
- SET FIPS_FLAGGER
dev_langs:
- TSQL
helpviewer_keywords:
- SET FIPS_FLAGGER statement
- FIPS 127-2 standard
- FIPS_FLAGGER option
ms.assetid: e82f6bee-6cf6-4061-be22-9ad2e8e9d3d6
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c28fd5419aec8bf15745150288b6878fd65ac1f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-fipsflagger-transact-sql"></a>SET FIPS_FLAGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica la comprobación del cumplimiento del estándar FIPS 127-2. Esto se basa en el estándar ISO. Para obtener información sobre la compatibilidad con SQL Server FIPS, consulte [cómo usar SQL Server 2016 en el modo FIPS 140-2-conforme](https://support.microsoft.com/help/4014354/how-to-use-sql-server-2016-in-fips-140-2-compliant-mode). 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET FIPS_FLAGGER ( 'level' |  OFF )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *nivel* **'**  
 Es el nivel de cumplimiento del estándar FIPS 127-2 que se comprueba en todas las operaciones de base de datos. Si una operación de base de datos está en conflicto con el nivel de estándares ISO elegido, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera una advertencia.  
  
 *nivel de* debe ser uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|ENTRY|Comprobación de los estándares ISO de compatibilidad con el nivel básico.|  
|FULL|Comprobación de los estándares ISO de compatibilidad plena.|  
|INTERMEDIATE|Comprobación de los estándares ISO de compatibilidad con el nivel intermedio.|  
|OFF|Sin comprobación del estándar.|  
  
## <a name="remarks"></a>Comentarios  
 El valor de `SET FIPS_FLAGGER` se establece en tiempo de análisis y no en ejecución o tiempo de ejecución. El establecimiento en tiempo de análisis significa que si la instrucción SET está presente en el lote o procedimiento almacenado, entrará en vigor, independientemente de si la ejecución de código no llegue al punto de control; y el `SET` instrucción surte efecto antes de que se ejecutan las instrucciones. Por ejemplo, incluso si la `SET` instrucción está en un `IF...ELSE` bloque de instrucciones que nunca se alcanza durante la ejecución, el `SET` tendrá efecto porque el `IF...ELSE` se analiza el bloque de instrucciones.  
  
 Si `SET FIPS_FLAGGER` se establece en un procedimiento almacenado, el valor de `SET FIPS_FLAGGER` se restaura cuando el control se devuelve desde el procedimiento almacenado. Por lo tanto, un `SET FIPS_FLAGGER` instrucción especificada en SQL dinámico no tiene ningún efecto en las instrucciones que sigue a la instrucción SQL dinámica.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

