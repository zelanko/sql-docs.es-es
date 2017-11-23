---
title: "Conexión de contexto | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5aba1b9a2ad2d70d56335e496e624864492397dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="context-connection"></a>Conexión de contexto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]El problema de acceso a datos internos es una situación bastante común. Es decir, desea tener acceso al mismo servidor en que se ejecuta el procedimiento almacenado o función de Common Language Runtime (CLR). Una opción consiste en crear una conexión mediante **System.Data.SqlClient.SqlConnection**, especifique una cadena de conexión que apunte al servidor local y abrir la conexión. Esto requiere especificar las credenciales para iniciar sesión. La conexión está en una sesión de base de datos diferente que el procedimiento almacenado o función, puede tener diferentes **establecer** opciones, está en una transacción independiente, no ve las tablas temporales, y así sucesivamente. Si el código del procedimiento almacenado administrado o de la función está en ejecución en el proceso de SQL Server, es porque alguien se ha conectado a ese servidor y ha ejecutado una instrucción SQL para invocarlo. Probablemente desea que el procedimiento almacenado o función que se ejecuta en el contexto de esa conexión, junto con su transacción, **establecer** opciones y así sucesivamente. Esto se denomina la conexión de contexto.  
  
 La conexión de contexto le permite ejecutar las instrucciones Transact-SQL en el mismo contexto que se invocó el código en primer lugar. Para obtener la conexión de contexto, debe utilizar la palabra clave de cadena de conexión "context connection", como en el ejemplo siguiente:  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>En esta sección  
 [Vs regulares. Conexiones de contexto](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Describe las diferencias que existen entre las conexiones normales y las conexiones de contexto.  
  
 [Restricciones en normales y conexiones de contexto](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Describe las restricciones en las conexiones normales y de contexto.  
  
  
