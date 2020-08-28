---
description: Especificar propiedades de conexión
title: Especificar propiedades de conexión | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c4d3a70388415402db3ecf8bdb21bd717a66aa6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979566"
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
