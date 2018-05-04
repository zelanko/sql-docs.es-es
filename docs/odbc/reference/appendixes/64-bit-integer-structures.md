---
title: Entero de 64 bits estructuras | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0f228bcaa8ec51491e2dad169e9e4cee88481f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="64-bit-integer-structures"></a>Estructuras de entero de 64 bits
El tipo de C para los identificadores de tipo de datos SQL_C_SBIGINT y SQL_C_UBIGINT en los compiladores de Microsoft C es _int64. Cuando se usa un compilador que no sea un compilador de C de Microsoft®, el tipo de C puede ser diferente. Si el compilador admite enteros de 64 bits de forma nativa, el controlador o la aplicación debe definir ODBCINT64 para que sea el tipo de entero de 64 bits nativo. Si el compilador no admite enteros de 64 bits de forma nativa, una aplicación o un controlador puede definir las siguientes estructuras para asegurarse de que tiene acceso a estos datos:  
  
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
  
 Estas estructuras deben alinearse a un límite de 8 bytes porque un entero de 64 bits se alinea con el límite de 8 bytes.
