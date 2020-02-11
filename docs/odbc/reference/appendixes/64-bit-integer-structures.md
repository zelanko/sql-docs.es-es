---
title: Estructuras de enteros de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d9e6fd01d6b9ef98ebb10f6728ec4ba205fbb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996258"
---
# <a name="64-bit-integer-structures"></a>Estructuras de entero de 64 bits
El tipo C para los identificadores de tipo de datos SQL_C_SBIGINT y SQL_C_UBIGINT en los compiladores de Microsoft C es _int64. Cuando se usa un compilador distinto de un compilador de Microsoft® C, el tipo C puede ser diferente. Si el compilador admite enteros de 64 bits de forma nativa, el controlador o la aplicación debe definir ODBCINT64 para que sea el tipo entero de 64 bits nativo. Si el compilador no admite enteros de 64 bits de forma nativa, una aplicación o un controlador puede definir las siguientes estructuras para asegurarse de que tiene acceso a estos datos:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 Estas estructuras se deben alinear con un límite de 8 bytes porque un entero de 64 bits se alinea con el límite de 8 bytes.
