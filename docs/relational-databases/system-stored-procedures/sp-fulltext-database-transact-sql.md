---
title: sp_fulltext_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ee0918a0b190b7b058f38eac4152dfb952f214bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771057"
---
# <a name="sp_fulltext_database-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, y solo se admite por razones de compatibilidad con versiones anteriores. **sp_fulltext_database** no deshabilita el motor de texto completo de una base de datos determinada. Todas las bases de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] creadas por el usuario están siempre habilitadas para la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Se usa [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @action = ] 'action'`Es la acción que se va a realizar. **Action** es de tipo **VARCHAR (20)** y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**enable**|Se admite únicamente por compatibilidad con versiones anteriores. No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.|  
|**disable**|Se admite únicamente por compatibilidad con versiones anteriores. No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, la indización de texto completo no se puede desactivar. Al deshabilitar la indización de texto completo no se quitan las filas de **sysfulltextcatalogs** y no se indica que las tablas habilitadas para texto completo ya no se marcan para la indización de texto completo. Todas las definiciones de metadatos de texto completo se mantienen en las tablas del sistema.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** y del rol fijo de base de datos **db_owner** pueden ejecutar **sp_fulltext_database**.  
  
## <a name="see-also"></a>Consulte también  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
