---
title: sp_article_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2670bd674589cf67acac91100d4419365de66da2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037757"
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia una solicitud de validación de datos del artículo especificado. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones y en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que incluye el artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo que se va a validar. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 Especifica si solamente se devuelve el recuento de filas de la tabla. *type_of_check_requested* es **smallint**, su valor predeterminado es **1**.  
  
 Si **0**, realizar un recuento de filas y un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 suma de comprobación compatible.  
  
 Si **1**, realizar solo una comprobación del recuento de filas.  
  
 Si **2**, realizar un recuento de filas y binario de suma de comprobación.  
  
 [  **@full_or_fast=**] *full_or_fast*  
 Es el método utilizado para calcular el recuento de filas. *full_or_fast* es **tinyint**, y puede tener uno de estos valores.  
  
|**Valor**|**Descripción**|  
|---------------|---------------------|  
|**0**|Realiza un recuento completo mediante COUNT(*).|  
|**1**|Realiza un recuento rápido de **sysindexes.rows**. Recuento de filas en **sysindexes** es más rápido que el recuento de filas en la tabla real. Sin embargo, **sysindexes** se actualiza de forma diferida, y el recuento de filas puede no ser exacto.|  
|**2** (predeterminado)|Realiza un recuento rápido condicional probando primero con el método rápido. Si el método rápido muestra diferencias, se utiliza el método completo. Si *expected_rowcount* es NULL y el procedimiento almacenado que se usa para obtener el valor, una completa COUNT(*) siempre se utiliza.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Especifica si el agente de distribución debe cerrarse inmediatamente cuando finalice la validación. *shutdown_agent* es **bit**, su valor predeterminado es **0**. Si **0**, el agente de distribución no se cierra. Si **1**, el agente de distribución se cierra después de validar el artículo.  
  
 [  **@subscription_level=**] *subscription_level*  
 Especifica si un conjunto de suscriptores recoge o no la validación. *subscription_level* es **bit**, su valor predeterminado es **0**. Si **0**, validación se aplica a todos los suscriptores. Si **1**, validación solo se aplica a un subconjunto de los suscriptores especificados mediante llamadas a **sp_marksubscriptionvalidation** en la transacción abierta actual.  
  
 [  **@reserved=**] *reservado*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica que no es[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse al solicitar la validación en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_article_validation** se utiliza en la replicación transaccional.  
  
 **sp_article_validation** hace que la información de validación se recopile en el artículo especificado y envía una solicitud de validación para el registro de transacciones. Cuando el Agente de distribución recibe la solicitud, compara la información de validación de la solicitud con la tabla del suscriptor. El resultado de la validación se muestra en el Monitor de replicación y en las alertas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permisos  
 Solo los usuarios con permisos selección ALL en la tabla de origen para el artículo que se está validando se puede ejecutar **sp_article_validation**.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos replicados](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
