---
title: "Método executeUpdate (java.lang.String) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a78fe10c14c54b5e2bea1cc4030a4f5d8d83fa1
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="executeupdate-method-javalangstring"></a>Método executeUpdate (java.lang.String)

Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE, MERGE o DELETE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL.

## <a name="syntax"></a>Sintaxis

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parámetros
*SQL*

A **cadena** que contiene la instrucción SQL.

## <a name="return-value"></a>Valor devuelto
Un **int** que indica el número de filas afectadas o 0 si se utiliza una instrucción DDL.

## <a name="exceptions"></a>Excepciones
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentarios
Este método executeUpdate es especificado por el método executeUpdate en la interfaz java.sql.PreparedStatement.

Llamar a este método producirá una excepción porque la instrucción SQL para el objeto SQLServerPreparedStatement no se especifica cuando se crea el objeto.

## <a name="see-also"></a>Vea también

[Método executeUpdate &#40; SQLServerPreparedStatement &#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[Miembros SQLServerPreparedStatement](./sqlserverpreparedstatement-members.md)

[Clase SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)
