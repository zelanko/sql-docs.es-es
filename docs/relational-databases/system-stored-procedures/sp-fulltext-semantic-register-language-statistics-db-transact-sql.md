---
title: sp_fulltext_semantic_register_language_statistics_db (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9b280110a6105ef136db387a2cdf64607ec9c11
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spfulltextsemanticregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra una base de datos previamente rellenada de estadísticas semánticas de lenguaje en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede iniciar la extracción semántica solo después de haber adjuntado esta base de datos de estadísticas de lenguaje y haberla registrado utilizando este procedimiento almacenado. Solo necesita realizar esta tarea una vez para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] ‘database_name’;  
GO  
```  
  
##  <a name="Arguments"></a> Argumentos  
 [ @dbname =] '*database_name*'  
 Es el nombre de la base de datos de estadísticas semánticas de lenguaje que se va a registrar para la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La base de datos debe estar ya adjunta. *database_name* es **sysname**, y no puede ser NULL.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno.  
  
## <a name="general-remarks"></a>Notas generales  
 La base de datos de estadísticas semánticas de lenguaje contiene estadísticas relacionadas con el lenguaje que se requieren para el procesamiento semántico de contenido de texto.  
  
 **sp_fulltext_semantic_register_language_statistics_db** realiza los pasos siguientes:  
  
1.  Comprueba que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una versión que admite el procesamiento semántico.  
  
2.  Comprueba que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene definida una base de datos de estadísticas semánticas de lenguaje.  
  
3.  Comprueba que la base de datos es una base de datos de estadísticas semánticas de lenguaje válida.  
  
4.  Establece permisos en la base de datos de estadísticas semánticas de lenguaje para restringir el acceso de los usuarios a la base de datos.  
  
5.  Inserta los metadatos que definen el nombre de la base de datos de estadísticas semánticas de lenguaje para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Inserta los metadatos que definen las asignaciones entre la base de datos de estadísticas semánticas de lenguaje instalada y las tablas internas de modelo de idioma.  
  
7.  Comprueba que la base de datos esté lista para usarse.  
  
 Para obtener más información, vea [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información acerca de la base de datos de estadísticas semánticas de lenguaje instalada en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte la vista de catálogo [sys.fulltext_semantic_language_statistics_database &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se requieren permisos CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo registrar la base de datos de estadísticas semánticas de lenguaje mediante una llamada a **sp_fulltext_semantic_register_language_statistics_db**.  
  
```tsql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
