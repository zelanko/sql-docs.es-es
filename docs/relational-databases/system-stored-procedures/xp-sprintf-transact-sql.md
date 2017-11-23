---
title: xp_sprintf (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs: TSQL
helpviewer_keywords: xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7619be5f36b1086609d4950ad0dad365d60a5a95
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="xpsprintf-transact-sql"></a>xp_sprintf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Da formato y almacena una serie de caracteres y valores en la cadena del parámetro de salida. Cada argumento de formato se sustituye por el argumento correspondiente.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *string*  
 Es un **varchar** variable que recibe la salida.  
  
 OUTPUT  
 Cuando se especifica, coloca el valor de la variable en el parámetro de salida.  
  
 *formato*  
 Es una cadena de caracteres de formato con marcadores de posición para *argumento* valores, similar a la que admiten el lenguaje c. **sprintf** función. Actualmente, solo se acepta el formato %s.  
  
 *argumento*  
 Es una cadena de caracteres que representa el valor del argumento de formato correspondiente.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar hasta 50 argumentos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_sprintf** devuelve el siguiente mensaje:  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Extendidos generales procedimientos almacenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  
