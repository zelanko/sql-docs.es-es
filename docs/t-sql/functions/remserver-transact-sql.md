---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0bc401b25b2822b7322c856ed3b2de0e670656b0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67944502"
---
# <a name="x40x40remserver-transact-sql"></a>&#x40;&#x40;REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilice servidores vinculados y procedimientos almacenados de servidores vinculados en su lugar.  
  
 Devuelve el nombre del servidor de base de datos remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tal y como aparece en el registro de inicio de sesión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Observaciones  
 @@REMSERVER permite a un procedimiento almacenado comprobar el nombre del servidor de base de datos desde el que se ejecuta.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea el procedimiento `usp_CheckServer` que devuelve el nombre del servidor remoto.  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 El siguiente procedimiento almacenado se crea en el servidor local `SEATTLE1`. El usuario inicia una sesión en un servidor remoto, `LONDON2`, y ejecuta `usp_CheckServer`.  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de configuración &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)  
  
  
