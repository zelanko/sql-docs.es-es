---
title: sp_publication_validation (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a310706bcc587838717064d1eb089cd044fc3375
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [**@publication=**] **' *** publicación '*  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@rowcount_only=**] *rowcount_only*  
 Indica si se devuelve solo el recuento de filas de la tabla. *rowcount_only* es **smallint** y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Realiza una suma de comprobación compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.<br /><br /> Nota: Cuando un artículo se filtra horizontalmente, se realiza una operación de recuento de filas en lugar de una operación de suma de comprobación.|  
|**1** (predeterminado)|Realiza solamente un recuento de filas.|  
|**2**|Realiza un recuento de filas y una suma de comprobación binaria.<br /><br /> Nota: Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores de la versión 7.0, solo una validación del recuento de filas se lleva a cabo.|  
  
 [**@full_or_fast=**] *full_or_fast*  
 Es el método utilizado para calcular el recuento de filas. *full_or_fast* es **tinyint** y puede tener uno de los siguientes valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Realiza un recuento completo mediante COUNT(*).|  
|**1**|Un recuento rápido desde **sysindexes.rows**. Recuento de filas en [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) es mucho más rápido que el recuento de filas en la tabla real. Sin embargo, dado que [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) forma diferida está actualizado, el recuento de filas puede no ser exacto.|  
|**2** (predeterminado)|Realiza un recuento rápido condicional intentando primero el método rápido. Si el método rápido muestra diferencias, se utiliza el método completo. Si *expected_rowcount* es NULL y el procedimiento almacenado se utiliza para obtener el valor, se utiliza siempre un Count completa.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 Indica si el agente de distribución se debe cerrar inmediatamente después de terminar la validación. *shutdown_agent* es **bits**, su valor predeterminado es **0**. Si **0**, el agente de replicación no se cierra. Si **1**, el agente de replicación se cierra después de valida el último artículo.  
  
 [ **@publisher** =] **'***publisher***'**  
 Especifica un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al solicitar la validación en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_publication_validation** se utiliza en la replicación transaccional.  
  
 **sp_publication_validation** se puede llamar en cualquier momento después de que se han activado los artículos asociados a la publicación. Se puede ejecutar el procedimiento una vez de forma manual, o bien como parte de un trabajo programado de forma regular que valide los datos.  
  
 Si la aplicación tiene suscriptores de actualización inmediata **sp_publication_validation** puede detectar falsos errores. **sp_publication_validation** calcula primero el recuento de filas o suma de comprobación en el publicador y, a continuación, en el suscriptor. Debido a que el desencadenador de actualización inmediata puede propagar una actualización al publicador desde el suscriptor, tras completar el recuento de filas o la suma de comprobación en el publicador pero antes de completarlas en el suscriptor, los valores podrían cambiar. Para asegurarse de que los valores del suscriptor y del publicador no cambian mientras se valida una publicación, detenga el servicio Microsoft DTC (Coordinador de transacciones distribuidas) en el publicador durante la validación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_publication_validation**.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
