---
title: SET TEXTSIZE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9925b382a7d09722846ca7da583fb92fe4609c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica el tamaño de **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **texto**, **ntext** , y **imagen** datos devueltos por una instrucción SELECT.  
  
> [!IMPORTANT]  
>  **ntext**, **texto**, y **imagen** tipos de datos se quitará en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite su uso en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que los usan actualmente. Use **nvarchar(max)**, **varchar(max)**y **varbinary(max)** en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argumentos  
 *number*  
 Es la longitud de **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **texto**, **ntext**, o **imagen** datos, en bytes. *número* es un entero con un valor máximo de 2147483647 (2 GB).  Un valor de -1 indica un tamaño ilimitado. El valor 0 restablece el tamaño en el valor predeterminado de 4 KB.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 y versiones posteriores) y el controlador ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificar automáticamente `-1` (ilimitado) conectarse.  
  
 **Controladores anteriores a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB (versión 9) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente TEXTSIZE en 2147483647 al conectarse.  
  
## <a name="remarks"></a>Comentarios  
 Configuración de SET TEXTSIZE afecta el @@TEXTSIZE función.  
  
 La opción de SET TEXTSIZE se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Vea también  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

