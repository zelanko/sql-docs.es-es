---
title: Limitaciones de la instrucción SELECT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26bf17596dbd3279498df2edcee7636db95ae139
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127854"
---
# <a name="select-statement-limitations"></a>Limitaciones de la instrucción SELECT
No se pueden mezclar una columna de la función de agregado con una columna que no sea de agregado en una instrucción SELECT.  
  
 La lista de selección de una instrucción SELECT que tenga una cláusula GROUP BY solo puede tener expresiones de la cláusula GROUP BY o conjunto de funciones.  
  
 No se admite el uso de un asterisco (para seleccionar todas las columnas) en una instrucción SELECT que contiene una cláusula GROUP BY. Se deben especificar los nombres de las columnas que se seleccionen.  
  
 No se admite el uso de una barra vertical en una instrucción SELECT. Usar un parámetro en la instrucción SELECT, si tiene que hacer referencia a un valor de datos que contiene una barra vertical.  
  
 Cuando se usa un alias de columna en una instrucción SELECT, la palabra "as" debe preceder a lo alias. Por ejemplo, "SELECT col1 como un de b." Sin el "ejemplo:" la instrucción devolverá un error.  
  
 Si se especifica un nombre de columna incorrecto en una instrucción SELECT, se devuelve un error de SQLSTATE 07001, "Número de parámetros incorrectos," en lugar de un error de SQLSTATE S0022 "columna no encontrada."  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, una cadena vacía se convierte en un valor NULL; una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no surtirán efecto en esa columna.
