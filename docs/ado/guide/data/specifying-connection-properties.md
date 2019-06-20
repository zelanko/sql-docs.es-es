---
title: Especificar propiedades de conexión | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 659701a984a675418b8654e9f747efe5d9e07762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700323"
---
# <a name="specifying-connection-properties"></a>Especificar propiedades de conexión
Puede proporcionar toda la información especificada por un [cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) estableciendo las propiedades de la **conexión** objeto antes de abrir la conexión. Por ejemplo, podría lograr el mismo efecto como se describe la cadena de conexión en [creación de una cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) con el código siguiente.  
  
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
>  En ADO no debe usar una contraseña que contenga el punto y coma (";") a menos que la contraseña se encierra entre comillas simples.
