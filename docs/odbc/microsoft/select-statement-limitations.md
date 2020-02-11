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
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987850"
---
# <a name="select-statement-limitations"></a>Limitaciones de la instrucción SELECT
Una columna de función de agregado no se puede mezclar con una columna no agregada en una instrucción SELECT.  
  
 La lista de selección de una instrucción SELECT que tiene una cláusula GROUP BY solo puede tener expresiones de la cláusula GROUP BY o de funciones set.  
  
 No se admite el uso de un asterisco (para seleccionar todas las columnas) en una instrucción SELECT que contenga una cláusula GROUP BY. Se deben especificar los nombres de las columnas que se van a seleccionar.  
  
 No se admite el uso de una barra vertical en una instrucción SELECT. Use un parámetro en la instrucción SELECT Si necesita hacer referencia a un valor de datos que contenga una barra vertical.  
  
 Cuando se usa un alias de columna en una instrucción SELECT, la palabra "as" debe preceder al alias. Por ejemplo, "seleccione col1 como a desde b". Sin "as", la instrucción devolverá un error.  
  
 Si se especifica un nombre de columna incorrecto en una instrucción SELECT, se devuelve un error SQLSTATE 07001, "número incorrecto de parámetros", en lugar de un error S0022 de SQLSTATE, "columna no encontrada".  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en un valor NULL. una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no se realizará correctamente en esa columna.
