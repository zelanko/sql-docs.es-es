---
title: sp_helparticlecolumns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3b5f5e70a599df333a4d00083929108f9a7172d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32995862"
---
# <a name="sphelparticlecolumns-transact-sql"></a>sp_helparticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve todas las columnas de la tabla subyacente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. En los publicadores de Oracle, este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación que contiene el artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo cuyas columnas se han devuelto. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe especificarse cuando se publica el artículo solicitado por un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (columnas que no están publicadas) o **1** (columnas que se publican)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Id. de columna**|**int**|Identificador de la columna.|  
|**column**|**sysname**|Nombre de la columna.|  
|**Publicado**|**bit**|Indica si la columna está publicada:<br /><br /> **0** = No<br /><br /> **1** = Sí|  
|**tipo de publicador**|**sysname**|Tipo de datos de la columna del publicador.|  
|**Tipo de suscriptor**|**sysname**|Tipo de datos de la columna del suscriptor.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_helparticlecolumns** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_helparticlecolumns** es útil para comprobar una partición vertical.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos o la lista de acceso de publicación para la publicación actual puede ejecutar **sp_helparticlecolumns**.  
  
## <a name="see-also"></a>Vea también  
 [Definir y modificar un filtro de columna](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
