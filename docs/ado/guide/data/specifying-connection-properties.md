---
title: "Especificar propiedades de conexión | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87bcb0bed714e3fd2719405fbd1887a7943d219d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
