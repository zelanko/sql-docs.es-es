---
title: "Método Execute (java.lang.String, int[]) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50cb9686b883ac0a4d682e7ea28f1dba40257c7e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
*SQL*

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

[Ejecutar método &#40; SQLServerStatement &#41;](./execute-method-sqlserverstatement.md)

[Miembros de SQLServerStatement](./sqlserverstatement-members.md)

[Clase SQLServerStatement](./sqlserverstatement-class.md)

