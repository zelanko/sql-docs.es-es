---
description: MSSQLSERVER_33129
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16340b6800ded7be2642f70496a09a16eb360274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456229"
---
# <a name="mssqlserver_33129"></a>MSSQLSERVER_33129
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|33129|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CANNOT_DISABLE_WIN_GROUP|  
|Texto del mensaje|No se puede usar ALTER_LOGIN con el argumento DISABLE para denegar el acceso a un grupo de Windows.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje se produce cuando se intenta deshabilitar el inicio de sesión de un grupo de Windows.  
  
## <a name="user-action"></a>Acción del usuario  
El inicio de sesión de un grupo de Windows no se puede deshabilitar. Para quitar temporalmente un permiso de acceso concedido a un grupo de Windows, REVOQUE el permiso CONNECT del inicio de sesión del grupo de Windows. Los usuarios de Windows quizá sigan teniendo acceso a través de su inicio de sesión individual o de otro grupo de Windows. En el siguiente ejemplo se revoca el permiso de conexión al grupo de contabilidad del dominio WESTCOAST.  
  
```Transact-SQL  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
