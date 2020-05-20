---
title: sp_helparticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c15a9051c6d706ddec55d031e93858a3d33c9d3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82815955"
---
# <a name="sp_helparticlecolumns-transact-sql"></a>sp_helparticlecolumns (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve todas las columnas de la tabla subyacente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. En los publicadores de Oracle, este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación que contiene el artículo. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'`Es el nombre del artículo en el que se devuelven las columnas. *article* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher = ] 'publisher'`Especifica un publicador que no es de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  no se debe especificar el *publicador* cuando un publicador publica el artículo solicitado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (columnas no publicadas) o **1** (columnas publicadas)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ID. de columna**|**int**|Identificador de la columna.|  
|**column**|**sysname**|Nombre de la columna.|  
|**sin**|**bit**|Indica si la columna está publicada:<br /><br /> **0** = no<br /><br /> **1** = sí|  
|**tipo de publicador**|**sysname**|Tipo de datos de la columna del publicador.|  
|**tipo de suscriptor**|**sysname**|Tipo de datos de la columna del suscriptor.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_helparticlecolumns** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_helparticlecolumns** es útil para comprobar una partición vertical.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , del rol fijo de base de datos **db_owner** o de la lista de acceso a la publicación para la publicación actual pueden ejecutar **sp_helparticlecolumns**.  
  
## <a name="see-also"></a>Consulte también  
 [Definir y modificar un filtro de columna](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [sp_addarticle &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_droppublication &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
