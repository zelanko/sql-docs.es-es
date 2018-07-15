---
title: Conexión de contexto | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
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
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5d464e257ca7d0f967dfbaf9325f3a30a30f0bc3
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356867"
---
# <a name="context-connection"></a>Conexión de contexto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El problema de acceso interno a los datos es un escenario bastante común. Es decir, desea tener acceso al mismo servidor en que se ejecuta el procedimiento almacenado o función de Common Language Runtime (CLR). Una opción consiste en crear una conexión mediante **System.Data.SqlClient.SqlConnection**, especifique una cadena de conexión que apunte al servidor local y abrir la conexión. Esto requiere especificar las credenciales para iniciar sesión. La conexión está en una sesión de base de datos diferente que el procedimiento almacenado o función, puede tener diferentes **establecer** opciones, está en una transacción independiente, no verá las tablas temporales, y así sucesivamente. Si el código del procedimiento almacenado administrado o de la función está en ejecución en el proceso de SQL Server, es porque alguien se ha conectado a ese servidor y ha ejecutado una instrucción SQL para invocarlo. Probablemente desea que el procedimiento almacenado o función que se ejecuta en el contexto de esa conexión, junto con su transacción, **establecer** opciones y así sucesivamente. Esto se denomina la conexión de contexto.  
  
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
 [Conexiones de contexto frente a conexiones normales](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Describe las diferencias que existen entre las conexiones normales y las conexiones de contexto.  
  
 [Conexiones de contexto y conexiones normales: restricciones](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Describe las restricciones en las conexiones normales y de contexto.  
  
  
