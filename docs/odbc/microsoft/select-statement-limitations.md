---
title: Limitaciones de la instrucción SELECT | Documentos de Microsoft
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
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e27e435fea1aeb864eb20ac478a72860394b8f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="select-statement-limitations"></a>Limitaciones de la instrucción SELECT
No se pueden mezclar una columna de la función de agregado con una columna no agregado en una instrucción SELECT.  
  
 La lista de selección de una instrucción SELECT que contiene una cláusula GROUP BY solo puede tener expresiones de la cláusula GROUP BY o funciones de conjunto.  
  
 No se admite el uso de un asterisco (para seleccionar todas las columnas) en una instrucción SELECT que contiene una cláusula GROUP BY. Deben especificarse los nombres de las columnas que desea seleccionar.  
  
 No se admite el uso de una barra vertical en una instrucción SELECT. Usar un parámetro en la instrucción SELECT si tiene que hacer referencia a un valor de datos que contiene una barra vertical.  
  
 Al utilizar un alias de columna en una instrucción SELECT, la palabra "as" debe preceder a lo alias. Por ejemplo, "SELECT col1 como un de b." Sin el "como" la instrucción devolverá un error.  
  
 Si se especifica un nombre de columna incorrecto en una instrucción SELECT, se devuelve un error de SQLSTATE 07001, "Número de parámetros incorrectos," en lugar de un error de SQLSTATE S0022, "columna no encontrada."  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en un valor NULL; una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no surtirán efecto en esa columna.
