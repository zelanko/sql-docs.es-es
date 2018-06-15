---
title: sp_helplanguage (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fdea1704b8942191bf79cb9074715f61eb9a9e81
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260438"
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de un idioma alternativo concreto o de todos los idiomas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@language=** ] **'***lenguaje***'**  
 Es el nombre del idioma alternativo para el que se muestra información. *idioma* es **sysname**, su valor predeterminado es null. Si *lenguaje* está especificado, se devuelve información sobre el idioma especificado. Si no se especifica el idioma, información acerca de todos los idiomas en el **sys.syslanguages** se devuelve la vista de compatibilidad.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**LangID**|**smallint**|Número de identificación del idioma.|  
|**dateformat**|**nchar(3)**|Formato de la fecha.|  
|**DATEFIRST**|**tinyint**|Primer día de la semana: 1 para lunes, 2 para martes y así sucesivamente hasta 7 para domingo.|  
|**Actualización**|**int**|Versión de la última actualización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este idioma.|  
|**Nombre**|**sysname**|Nombre del idioma.|  
|**alias**|**sysname**|Nombre alternativo del idioma.|  
|**Meses**|**nvarchar(372)**|Nombres de los meses.|  
|**SHORTMONTHS**|**nvarchar(132)**|Abreviaturas de los nombres de los meses.|  
|**Días**|**nvarchar(217)**|Nombres de los días.|  
|**lcid**|**int**|Id. de configuración regional de Windows para el idioma.|  
|**msglangid**|**smallint**|Identificador del grupo de mensajes del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-information-about-a-single-language"></a>A. Devolver información acerca de un solo idioma  
 El ejemplo siguiente muestra información acerca del idioma alternativo `French`.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. Devolver información acerca de todos los idiomas  
 El siguiente ejemplo muestra información acerca de todos los idiomas alternativos instalados.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
