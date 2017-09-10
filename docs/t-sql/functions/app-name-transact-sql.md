---
title: App_name (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4f63ae216bad0269415ac5e0aa57a7543500f0c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el nombre de aplicación de la sesión actual si la aplicación lo ha establecido.
  
> [!IMPORTANT]  
>  El nombre de la aplicación lo proporciona el cliente y no está verificado de ninguna manera. No utilice **APP_NAME** como parte de una comprobación de seguridad.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
**nvarchar (128)**
  
## <a name="remarks"></a>Comentarios  
Use **APP_NAME** cuando desee realizar acciones diferentes para distintas aplicaciones. Por ejemplo, formatear una fecha de diferentes maneras para diferentes aplicaciones o devolver un mensaje informativo a ciertas aplicaciones.
  
Para establecer un nombre de aplicación en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], en la **conectar al motor de base de datos** cuadro de diálogo, haga clic en **opciones**. En el **parámetros de conexión adicionales** ficha, proporcione un **aplicación** atributo con el formato`;app='application_name'`
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se comprueba si la aplicación del cliente que ha iniciado este proceso es una sesión `SQL Server Management Studio` y proporciona una fecha en formato estadounidense o ANSI.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Vea también
[Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Funciones](../../t-sql/functions/functions.md)
  
  

