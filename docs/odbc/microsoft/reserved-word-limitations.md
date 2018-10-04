---
title: Reservado limitaciones de Word | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 531a100fed389264d9af6a1733636792a3dc7920
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764493"
---
# <a name="reserved-keyword-limitations"></a>Limitaciones de la palabra clave reservada

Evite usar palabras clave reservada de ODBC como identificadores en las tablas SQL o los objetos relacionados. Si un caso impar surge donde debe usar una palabra clave reservada como identificador, se debe encerrar el identificador con un par de *graves* ('). Otro nombre para *acento grave* es *comilla inversa*.

La limitación de la palabra clave reservada también se aplica a cualquier forma abreviada de las palabras clave reservadas.

Una lista de las palabras clave reservada de ODBC está disponible en:

- [Palabras clave reservadas de ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- En el *Guía de referencia del programador de ODBC*, consulte [Apéndice C: SQL gramática](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

