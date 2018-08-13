---
title: xp_sprintf (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e8d0683523c12e4379b78e9fa92fb70d6d869051
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556486"
---
# <a name="xpsprintf-transact-sql"></a>xp_sprintf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Da formato y almacena una serie de caracteres y valores en la cadena del parámetro de salida. Cada argumento de formato se sustituye por el argumento correspondiente.  
  
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
  
 *format*  
 Es una cadena de caracteres de formato con marcadores de posición para *argumento* valores, similares a la que admite el lenguaje c. **sprintf** función. Actualmente, solo se acepta el formato %s.  
  
 *argument*  
 Es una cadena de caracteres que representa el valor del argumento de formato correspondiente.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar hasta 50 argumentos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_sprintf** devuelve el siguiente mensaje:  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  
