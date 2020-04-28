---
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d6952d245dfc9083c7cfa6e6d36ad991ffd24654
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72909139"
---
# <a name="sp_fulltext_semantic_unregister_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cancela el registro de una base de datos existente de estadísticas semánticas de lenguaje de la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y elimina los metadatos asociados.  
  
 Esta instrucción no separa la base de datos ni quita el archivo de base de datos físico del sistema de archivos. Después de cancelar el registro de la base de datos, puede separarla y eliminar el archivo de base de datos físico.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 Este procedimiento no requiere argumentos. Dado que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo tiene una base de datos de estadísticas semánticas de lenguaje, no es necesario identificar la base de datos.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-set"></a>Tipo de cursor  
 Ninguno.  
  
## <a name="general-remarks"></a>Notas generales  
 Cuando se cancela el registro de una base de datos de estadísticas semánticas de lenguaje, también se quitan todos los metadatos asociados a ella.  
  
 **sp_fulltext_semantic_unregister_language_statistics_db** realiza los pasos siguientes:  
  
1.  Comprueba que no haya rellenados semánticos en curso para la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Quita todos los metadatos asociados a la base de datos especificada de estadísticas semánticas de lenguaje.  

 Para obtener más información, vea [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información acerca de la base de datos de Estadísticas de lenguaje semántico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instalada en una instancia de, consulte la vista de catálogo [sys. fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Se requieren permisos CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo anular el registro de la base de datos Estadísticas de lenguaje semántico llamando a **sp_fulltext_semantic_unregister_language_statistics_db**.  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
