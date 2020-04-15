---
title: ¡Limitaciones de la declaración CREATE INDEX ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280886"
---
# <a name="create-index-statement-limitations"></a>CREAR las limitaciones de la instrucción de índice
La instrucción CREATE INDEX no se admite para los controladores de Microsoft Excel o Text.  
  
 Un índice se puede definir en un máximo de 10 columnas. Si se incluyen más de 10 columnas en una instrucción CREATE INDEX, el índice no se reconocerá y la tabla se tratará como si no se creara ningún índice.  
  
 El controlador dBASE no puede crear un índice en una columna LOGICAL.  
  
 Cuando se utiliza el controlador dBASE, el tiempo de respuesta en archivos grandes se puede mejorar mediante la creación de un índice .mdx (o .ndx) en la columna (campo) especificada en las cláusulas WHERE de una instrucción SELECT. Los índices .mdx existentes se aplicarán \<automáticamente a los operadores de .mdx, >, , >, ,< y BETWEEN en una cláusula WHERE y predicados LIKE, así como en predicados de combinación.  
  
 Cuando se utiliza el controlador dBASE, el índice creado por una instrucción CREATE UNIQUE INDEX no es realmente único y se pueden insertar valores duplicados en la columna indizada. Solo se puede agregar un registro de un conjunto con valores de clave idénticos al índice.  
  
 Cuando se utiliza el controlador Paradox, se debe definir un índice único en un subconjunto contiguo de las columnas de una tabla, incluida la primera columna. El controlador Paradox no puede actualizar una tabla si no se define un índice único en la tabla o cuando se utiliza el controlador Paradox sin la implementación del motor de base de datos de Borland.
