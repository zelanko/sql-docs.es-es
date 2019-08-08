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
ms.openlocfilehash: 4b1522a64d43256660966341ebe43f8d4ac4e0be
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771161"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
 **[@publication=** ] **'** _publicación '_  
 Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
 [ **@rowcount_only=** ] *rowcount_only*  
 Indica si se devuelve solo el recuento de filas de la tabla. *rowcount_only* es **smallint** y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Realiza una suma de comprobación compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.<br /><br /> Nota: Cuando un artículo se filtra horizontalmente, se realiza una operación de recuento de filas en lugar de una operación de suma de comprobación.|  
|**1** (predeterminado)|Realiza solamente un recuento de filas.|  
|**2**|Realiza un recuento de filas y una suma de comprobación binaria.<br /><br /> Nota: En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el caso de los suscriptores de la versión 7,0, solo se realiza una validación del recuento de filas.|  
  
 **[@full_or_fast=** ] *full_or_fast*  
 Es el método utilizado para calcular el recuento de filas. *full_or_fast* es **tinyint** y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Realiza un recuento completo mediante COUNT(*).|  
|**1**|Realiza un recuento rápido de **sysindexes. Rows**. Contar las filas en [Sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) es mucho más rápido que contar las filas de la tabla real. Sin embargo, dado que [Sys. sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) se actualiza de forma diferida, es posible que el recuento de filas no sea preciso.|  
|**2** (predeterminado)|Realiza un recuento rápido condicional intentando primero el método rápido. Si el método rápido muestra diferencias, se utiliza el método completo. Si *expected_rowcount* es NULL y se usa el procedimiento almacenado para obtener el valor, siempre se usa un recuento completo (*).|  
  
`[ @shutdown_agent = ] shutdown_agent`Indica si el Agente de distribución debe cerrarse inmediatamente al completarse la validación. *shutdown_agent* es de **bit**y su valor predeterminado es **0**. Si es **0**, el agente de replicación no se cierra. Si es **1**, el agente de replicación se cierra después de validar el último artículo.  
  
`[ @publisher = ] 'publisher'`Especifica un publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no es de. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  no se debe usar el publicador al solicitar la validación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_publication_validation** se utiliza en la replicación transaccional.  
  
 se puede llamar a **sp_publication_validation** en cualquier momento después de activar los artículos asociados a la publicación. Se puede ejecutar el procedimiento una vez de forma manual, o bien como parte de un trabajo programado de forma regular que valide los datos.  
  
 Si la aplicación tiene suscriptores de actualización inmediata, **sp_publication_validation** puede detectar falsos errores. **sp_publication_validation** calcula primero el recuento de filas o la suma de comprobación en el publicador y, a continuación, en el suscriptor. Debido a que el desencadenador de actualización inmediata puede propagar una actualización al publicador desde el suscriptor, tras completar el recuento de filas o la suma de comprobación en el publicador pero antes de completarlas en el suscriptor, los valores podrían cambiar. Para asegurarse de que los valores del suscriptor y del publicador no cambian mientras se valida una publicación, detenga el servicio Microsoft DTC (Coordinador de transacciones distribuidas) en el publicador durante la validación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_publication_validation**.  
  
## <a name="see-also"></a>Vea también  
 [Validar datos en el suscriptor](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
