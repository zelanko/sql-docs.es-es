---
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9d9652c25875fb1edb5d09e4e283fd7393b523a6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Una función que devuelve el nombre de aplicación de la sesión actual si la aplicación establece ese valor de nombre.
  
> [!IMPORTANT]  
>  El cliente proporciona el nombre de la aplicación y el valor del nombre de la aplicación no se verifica de ninguna manera. No use **APP_NAME** como parte de una comprobación de seguridad.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
**nvarchar(128)**
  
## <a name="remarks"></a>Notas  
Use **APP_NAME** para distinguir entre diferentes aplicaciones, como una manera de realizar acciones diferentes para esas aplicaciones. Por ejemplo, **APP_NAME** puede distinguir entre diferentes aplicaciones para permitir un formato de fecha diferente para cada aplicación. También puede permitir el envío de un mensaje informativo a ciertas aplicaciones.
  
Para establecer el nombre de una aplicación en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic en **Opciones** en el cuadro de diálogo **Conectar al motor de base de datos**. En la pestaña **Parámetros de conexión adicionales**, indique un atributo **app** con el formato `;app='application_name'`.
  
## <a name="example"></a>Ejemplo  
En este ejemplo se comprueba si la aplicación del cliente que ha iniciado este proceso es una sesión `SQL Server Management Studio` y proporciona una fecha en formato estadounidense o ANSI.
  
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
[Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Funciones](../../t-sql/functions/functions.md)
  
  
