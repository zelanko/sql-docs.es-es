---
title: Conexión de contexto | Microsoft Docs
description: En Microsoft SQL Server, la conexión de contexto permite ejecutar instrucciones Transact-SQL en el mismo contexto en el que se invocó el código.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4d6b6f8e37dca038c25cb9afe86f97d86e4e3121
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717939"
---
# <a name="context-connection"></a>Conexión de contexto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  El problema de acceso interno a los datos es un escenario bastante común. Es decir, desea tener acceso al mismo servidor en que se ejecuta el procedimiento almacenado o función de Common Language Runtime (CLR). Una opción consiste en crear una conexión con **System. Data. SqlClient. SqlConnection**, especificar una cadena de conexión que señale al servidor local y abrir la conexión. Esto requiere especificar las credenciales para iniciar sesión. La conexión está en una sesión de base de datos diferente que la función o el procedimiento almacenado, puede tener diferentes opciones **set** , está en una transacción independiente, no ve las tablas temporales, etc. Si el código del procedimiento almacenado administrado o de la función está en ejecución en el proceso de SQL Server, es porque alguien se ha conectado a ese servidor y ha ejecutado una instrucción SQL para invocarlo. Probablemente desee que el procedimiento almacenado o la función se ejecuten en el contexto de esa conexión, junto con su transacción, las opciones **set** , etc. Esto se denomina la conexión de contexto.  
  
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
 [Conexiones normales y conexiones de contexto](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 Describe las diferencias que existen entre las conexiones normales y las conexiones de contexto.  
  
 [Conexiones de contexto y conexiones normales: restricciones](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 Describe las restricciones en las conexiones normales y de contexto.  
  
  
