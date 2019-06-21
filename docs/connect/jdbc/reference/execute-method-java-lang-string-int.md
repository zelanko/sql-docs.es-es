---
title: Método Execute (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d4ae744a27156a59c926f2181ca9aec1146e8cd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801660"
---
# <a name="execute-method-javalangstring-int"></a>Método execute (java.lang.String, int[])

  Ejecuta la instrucción SQL especificada, que puede devolver varios resultados, e indica al [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que las claves que se han generado automáticamente y están presentes en la matriz dada deben estar disponibles para su recuperación.

## <a name="syntax"></a>Sintaxis

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parámetros
*sql*

Un valor **String** que contiene una instrucción SQL.

*columnIndexes*

Una matriz de valores **int** que indica que los índices de columna de las claves que se generaron automáticamente deben estar disponibles.

## <a name="return-value"></a>Valor devuelto
**True** si el primer resultado es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.
  
## <a name="exceptions"></a>Excepciones
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Notas
El método execute especifica este método execute en la interfaz java.sql.Statement.

## <a name="see-also"></a>Consulte también

[Método Execute &#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[Miembros SQLServerStatement](./sqlserverstatement-members.md)

[Clase SQLServerStatement](./sqlserverstatement-class.md)
