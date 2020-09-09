---
description: sp_ivindexhasnullcols (Transact-SQL)
title: sp_ivindexhasnullcols (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fe91514a87999bb053f6011e74b3b96ec075fbf4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549629"
---
# <a name="sp_ivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Comprueba que el índice clúster de la vista indizada es exclusivo y no contiene ninguna columna que pueda tener el valor NULL cuando se vaya a utilizar la vista indizada para crear una publicación transaccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @viewname = ] 'view_name'` Es el nombre de la vista que se va a comprobar. *view_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` Es la marca que indica si el índice de la vista tiene columnas que permiten valores NULL. *view_name* es de **tipo sysname**y no tiene ningún valor predeterminado. Devuelve el valor **1** si el índice de la vista tiene columnas que permiten valores NULL. Devuelve un valor de **0** si la vista no contiene columnas que permitan valores NULL.  
  
> [!NOTE]  
>  Si el propio procedimiento almacenado devuelve un código de retorno de **1**, lo que significa que se ha producido un error en la ejecución del procedimiento almacenado, este valor es **0** y debe omitirse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 la replicación transaccional utiliza **sp_ivindexhasnullcols** .  
  
 De manera predeterminada, los artículos de vista indizada de una publicación se crean como tablas en los suscriptores. Sin embargo, cuando la columna indizada permite valores NULL, la vista indizada se crea como una vista indizada en el suscriptor en lugar de una tabla. Al ejecutar este procedimiento almacenado, se puede alertar al usuario sobre si existe o no este problema con la vista indizada actual.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_ivindexhasnullcols**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
