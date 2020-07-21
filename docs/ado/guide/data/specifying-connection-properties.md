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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fee9745bca206f00603b32a6c4cd29faab34eca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760841"
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
