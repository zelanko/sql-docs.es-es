---
title: Método prepareStatement (java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afd095efadf10a6838fb5ba8f6abec6a6f9e0bb5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="preparestatement-method-javalangstring"></a>Método prepareStatement (java.lang.String)

Crea un [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) objeto para enviar instrucciones SQL parametrizadas a la base de datos.

## <a name="syntax"></a>Sintaxis

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parámetros
*sql*

A **cadena** que contiene una instrucción SQL.

## <a name="return-value"></a>Valor devuelto
Un objeto de instrucción PreparedStatement.

## <a name="exceptions"></a>Excepciones  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentarios
Este método prepareStatement especificado por el método prepareStatement en la interfaz java.sql.Connection.

## <a name="see-also"></a>Vea también

[Método prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Miembros SQLServerConnection](./sqlserverconnection-members.md)

[Clase SQLServerConnection](./sqlserverconnection-class.md)
