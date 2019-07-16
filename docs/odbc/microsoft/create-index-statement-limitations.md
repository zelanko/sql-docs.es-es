---
title: CREAR las limitaciones de la instrucción de índice | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ddb695d996cdd40b7fde4087799e5c1ec84224c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081927"
---
# <a name="create-index-statement-limitations"></a>CREAR las limitaciones de la instrucción de índice
La instrucción CREATE INDEX no se admite para los controladores de Microsoft Excel o texto.  
  
 Un índice puede definirse en un máximo de 10 columnas. Si más de 10 columnas se incluyen en una instrucción CREATE INDEX, no se reconocerá el índice y la tabla se tratará como si no se crearon ningún índice.  
  
 El controlador de dBASE no puede crear un índice en una columna lógica.  
  
 Cuando se usa el controlador de dBASE, se puede mejorar el tiempo de respuesta en los archivos de gran tamaño mediante la creación de un índice .mdx (o ndx) en la columna (campo) especificado en las cláusulas WHERE de una instrucción SELECT. Los índices .mdx existentes se aplicarán automáticamente para =, >, \<, > =, = < y entre los operadores en una cláusula WHERE y los predicados LIKE, así como en los predicados de combinación.  
  
 Cuando se usa el controlador de dBASE, el índice creado por una instrucción CREATE UNIQUE INDEX es en realidad no es único y se pueden insertar valores duplicados en la columna indizada. Sólo un registro de un conjunto con idénticos valores de clave se puede agregar al índice.  
  
 Cuando se usa el controlador de Paradox, se debe definir un índice único en un subconjunto de las columnas en una tabla, incluida la primera columna contiguo. Una tabla no se puede actualizar el controlador de Paradox si un índice único no está definido en la tabla o cuando se utiliza el controlador de Paradox sin la implementación del motor de base de datos Borland.
