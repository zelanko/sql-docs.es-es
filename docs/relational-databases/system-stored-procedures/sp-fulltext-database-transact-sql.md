---
title: sp_fulltext_database (Transact-SQL) | Microsoft Docs
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
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 5ee4cb63c476b898c286f6223e9e56d1778e6a47
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563909"
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, y solo se admite por razones de compatibilidad con versiones anteriores. **sp_fulltext_database** no deshabilita el motor de texto completo para una base de datos. Todas las bases de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] creadas por el usuario están siempre habilitadas para la indización de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@action=**] **'***acción***'**  
 Se trata de la acción que se va a realizar. **acción** es **varchar (20)**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**habilitar**|Se admite únicamente por compatibilidad con versiones anteriores. No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.|  
|**disable**|Se admite únicamente por compatibilidad con versiones anteriores. No tiene ningún efecto en catálogos de texto completo en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Notas  
 En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, la indización de texto completo no se puede desactivar. Deshabilitar indización de texto completo no quita las filas de **sysfulltextcatalogs** y no indica que las tablas habilitadas para texto completo ya no están marcadas para la indización de texto completo. Todas las definiciones de metadatos de texto completo se mantienen en las tablas del sistema.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor y **db_owner** rol fijo de base de datos se puede ejecutar **sp_fulltext_database**.  
  
## <a name="see-also"></a>Vea también  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
