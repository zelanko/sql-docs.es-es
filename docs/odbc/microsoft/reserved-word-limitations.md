---
title: Limitaciones de palabras reservadas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304013"
---
# <a name="reserved-keyword-limitations"></a>Limitaciones de palabras clave reservadas

Evite usar palabras clave reservadas ODBC como identificadores en las tablas SQL u objetos relacionados. Si surge un caso impar en el que debe utilizar una palabra clave reservada como identificador, debe rodear el identificador con un par de *backticks* ('). Otro nombre para *backtick* es *back quote*.

La limitación de palabras clave reservadas también se aplica a cualquier forma abreviada de las palabras clave reservadas.

Una lista de las palabras clave reservadas ODBC está disponible en:

- [Palabras clave reservadas ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- En la *Guía de referencia del programador ODBC*, vea Apéndice [C: Gramática SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

