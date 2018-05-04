---
title: Método Execute (java.lang.String, int[]) | Documentos de Microsoft
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
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 046bcaa04b4bbc84faf7d8499618059dc5ed42af
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="execute-method-javalangstring-int"></a>Método execute (java.lang.String, int[])

  Ejecuta la instrucción SQL determinada, que puede devolver varios resultados e indica [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)] que las claves generadas automáticamente que se indican en la matriz especificada deben estar disponibles para la recuperación.

## <a name="syntax"></a>Sintaxis

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parámetros
*sql*

A **cadena** que contiene una instrucción SQL.

*columnIndexes*

Una matriz de **int**que indica los índices de columna de las claves generadas automáticamente que deben estar disponibles.

## <a name="return-value"></a>Valor devuelto
**True** si el primer resultado es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.
  
## <a name="exceptions"></a>Excepciones
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentarios
Este método de ejecución especificado por el método execute en la interfaz java.sql.Statement.

## <a name="see-also"></a>Vea también

[ejecutar el método &#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[Miembros de SQLServerStatement](./sqlserverstatement-members.md)

[Clase SQLServerStatement](./sqlserverstatement-class.md)
