---
title: Especificar propiedades de conexión | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8aea80d0bd512d75e46686722242d4955baa4769
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="specifying-connection-properties"></a>Especificar propiedades de conexión
Puede proporcionar toda la información especificada por un [cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) estableciendo las propiedades de la **conexión** objeto antes de abrir la conexión. Por ejemplo, podría conseguir el mismo efecto como la cadena de conexión se describe en [crear una cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) utilizando el código siguiente.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase se establece solo después de abrir la conexión.  
  
> [!NOTE]
>  En ADO no deben usar una contraseña que contenga el punto y coma (";") a menos que la contraseña se encierra entre comillas simples.
