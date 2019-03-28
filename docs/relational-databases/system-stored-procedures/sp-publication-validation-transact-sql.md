---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 124d5d14f810a32e32ce92cbb96afe4569804c67
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537177"
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia una solicitud de validación de cada uno de los artículos de la publicación especificada. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publication=**] **'**_publicación '_  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@rowcount_only=**] *rowcount_only*  
 Indica si se devuelve solo el recuento de filas de la tabla. *rowcount_only* es **smallint** y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Realiza una suma de comprobación compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.<br /><br /> Nota: Cuando un artículo se filtra horizontalmente, se realiza una operación de recuento de filas en vez de una operación de suma de comprobación.|  
|**1** (predeterminado)|Realiza solamente un recuento de filas.|  
|**2**|Realiza un recuento de filas y una suma de comprobación binaria.<br /><br /> Nota: Para suscriptores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0, solo se realiza la validación de recuento de filas.|  
  
 [**@full_or_fast=**] *full_or_fast*  
 Es el método utilizado para calcular el recuento de filas. *full_or_fast* es **tinyint** y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Realiza un recuento completo mediante COUNT(*).|  
|**1**|Un recuento rápido desde **sysindexes.rows**. Recuento de filas en [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) es mucho más rápido que el recuento de filas en la tabla real. Sin embargo, dado que [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) constantemente actualizado, el recuento de filas puede no ser exacto.|  
|**2** (predeterminado)|Realiza un recuento rápido condicional intentando primero el método rápido. Si el método rápido muestra diferencias, se utiliza el método completo. Si *expected_rowcount* es NULL y el procedimiento almacenado que se usa para obtener el valor, una completa COUNT(*) siempre se utiliza.|  
  
`[ @shutdown_agent = ] shutdown_agent` Indica si el agente de distribución debe cerrar inmediatamente tras la finalización de la validación. *shutdown_agent* es **bit**, su valor predeterminado es **0**. Si **0**, el agente de replicación no se cierra. Si **1**, el agente de replicación se cierra después de valida el último artículo.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse al solicitar la validación en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_publication_validation** se utiliza en la replicación transaccional.  
  
 **sp_publication_validation** puede llamarse en cualquier momento después de que se han activado los artículos asociados con la publicación. Se puede ejecutar el procedimiento una vez de forma manual, o bien como parte de un trabajo programado de forma regular que valide los datos.  
  
 Si la aplicación tiene suscriptores de actualización inmediata **sp_publication_validation** puede detectar falsos errores. **sp_publication_validation** calcula primero el recuento de filas o suma de comprobación en el publicador y, a continuación, en el suscriptor. Debido a que el desencadenador de actualización inmediata puede propagar una actualización al publicador desde el suscriptor, tras completar el recuento de filas o la suma de comprobación en el publicador pero antes de completarlas en el suscriptor, los valores podrían cambiar. Para asegurarse de que los valores del suscriptor y del publicador no cambian mientras se valida una publicación, detenga el servicio Microsoft DTC (Coordinador de transacciones distribuidas) en el publicador durante la validación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_publication_validation**.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
