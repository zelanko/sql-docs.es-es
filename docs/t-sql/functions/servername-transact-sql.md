---
title: '@@SERVERNAME (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 93d03e11df97075b2d608d7bfcc4e234c37971cd
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el nombre del servidor local que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar**  
  
## <a name="remarks"></a>Comentarios  
 El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establece durante la instalación el nombre del equipo como nombre de servidor. Para cambiar el nombre del servidor, utilice **sp_addserver**y, a continuación, reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Con varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada, @@SERVERNAME devuelve el siguiente servidor local de información de nombre si no se cambió el nombre del servidor local desde el programa de instalación.  
  
|Instancia|Información de servidor|  
|--------------|------------------------|  
|Instancia predeterminada|'*servername*'|  
|Instancia con nombre|'*servername*\\*nombreDeInstancia*'|  
|instancia en clúster de conmutación por error: instancia predeterminada|'*nombreDeServidorVirtual*'|  
|instancia en clúster de conmutación por error: instancia con nombre|'*nombreDeServidorVirtual*\\*nombreDeInstancia*'|  
  
 Aunque el @@SERVERNAME función y la propiedad SERVERNAME de la función SERVERPROPERTY pueden devolver cadenas con formatos similares, la información puede ser diferente. La propiedad SERVERNAME informa automáticamente de los cambios en el nombre de red del equipo.  
  
 En cambio, @@SERVERNAME no informa de estos cambios. @@SERVERNAME informa de los cambios realizados en el nombre de servidor local mediante la **sp_addserver** o **sp_dropserver** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra la forma de utilizar `@@SERVERNAME`.  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo.  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  

