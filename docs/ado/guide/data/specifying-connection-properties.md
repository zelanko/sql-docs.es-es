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
ms.openlocfilehash: 5aee5946f3087956a0117b88f4044ef8a6c9bd9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924138"
---
# <a name="specifying-connection-properties"></a>Especificar propiedades de conexión
Puede proporcionar gran parte de la información especificada por una [cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) estableciendo las propiedades del objeto de **conexión** antes de abrir la conexión. Por ejemplo, podría lograr el mismo efecto que la cadena de conexión que se describe en [crear una cadena de conexión](../../../ado/guide/data/creating-a-connection-string.md) mediante el código siguiente.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase solo se establece después de abrir la conexión.  
  
> [!NOTE]
>  En ADO, no debe utilizar una contraseña que contenga signos de punto y coma (";"), a menos que la contraseña se incluya entre comillas simples.
