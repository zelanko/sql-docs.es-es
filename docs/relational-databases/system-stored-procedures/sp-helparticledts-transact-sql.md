---
title: sp_helparticledts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cac631425a43870395fa0adceb0bb041d70e1932
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62797260"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para obtener información sobre los nombres de tarea personalizada correctos que se deben utilizar cuando se cree una suscripción de transformación con [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'` Es el nombre de un artículo de la publicación. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|Nombre de la tarea de programación que tiene lugar antes de que se copien los datos de la instantánea. La ejecución del programa debe continuar si se encuentra un error de script.|  
|**pre_script_task_name**|**sysname**|Nombre de la tarea de programación que tiene lugar antes de que se copien los datos de la instantánea. La ejecución del programa se detiene si encuentra un error.|  
|**transformation_task_name**|**sysname**|Nombre de la tarea de programación cuando se utiliza una tarea de consulta controlada por datos.|  
|**post_script_ignore_error_task_name**|**sysname**|Nombre de la tarea de programación que tiene lugar después de copiarse los datos de la instantánea. La ejecución del programa debe continuar si se encuentra un error de script.|  
|**post_script_task_name**|**sysname**|Nombre de la tarea de programación que tiene lugar después de copiarse los datos de la instantánea. La ejecución del programa se detiene si encuentra un error.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helparticledts** se utiliza en la replicación de instantáneas y transaccional.  
  
 Existen convenciones de nomenclatura, necesarias para los agentes de replicación, que se deben seguir cuando se da nombre a las tareas de un programa de Servicios de transformación de datos (DTS) de replicación. En las tareas personalizadas, como una tarea Ejecutar SQL, el nombre es una cadena concatenada que consta del nombre del artículo, un prefijo y una parte opcional. Al escribir el código, si no está seguro de cómo deben ser los nombres de tarea, el conjunto de resultados proporciona los nombres de tarea que se deben utilizar.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helparticledts**.  
  
  
