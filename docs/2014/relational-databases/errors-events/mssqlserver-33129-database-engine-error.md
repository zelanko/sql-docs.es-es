---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 60be94308520f93c76f28ef5e0d1bbbf474dfdbd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063745"
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33129|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CANNOT_DISABLE_WIN_GROUP|  
|Texto del mensaje|No se puede usar ALTER_LOGIN con el argumento DISABLE para denegar el acceso a un grupo de Windows.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje se produce cuando se intenta deshabilitar el inicio de sesión de un grupo de Windows.  
  
## <a name="user-action"></a>Acción del usuario  
 El inicio de sesión de un grupo de Windows no se puede deshabilitar. Para quitar temporalmente un permiso de acceso concedido a un grupo de Windows, REVOQUE el permiso CONNECT del inicio de sesión del grupo de Windows. Los usuarios de Windows quizá sigan teniendo acceso a través de su inicio de sesión individual o de otro grupo de Windows. En el siguiente ejemplo se revoca el permiso de conexión al grupo de contabilidad del dominio WESTCOAST.  
  
```tsql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  
