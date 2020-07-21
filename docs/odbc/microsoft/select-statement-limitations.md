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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300925"
---
# <a name="select-statement-limitations"></a>Limitaciones de la instrucción SELECT
Una columna de función de agregado no se puede mezclar con una columna no agregada en una instrucción SELECT.  
  
 La lista de selección de una instrucción SELECT que tiene una cláusula GROUP BY solo puede tener expresiones de la cláusula GROUP BY o de funciones set.  
  
 No se admite el uso de un asterisco (para seleccionar todas las columnas) en una instrucción SELECT que contenga una cláusula GROUP BY. Se deben especificar los nombres de las columnas que se van a seleccionar.  
  
 No se admite el uso de una barra vertical en una instrucción SELECT. Use un parámetro en la instrucción SELECT Si necesita hacer referencia a un valor de datos que contenga una barra vertical.  
  
 Cuando se usa un alias de columna en una instrucción SELECT, la palabra "as" debe preceder al alias. Por ejemplo, "seleccione col1 como a desde b". Sin "as", la instrucción devolverá un error.  
  
 Si se especifica un nombre de columna incorrecto en una instrucción SELECT, se devuelve un error SQLSTATE 07001, "número incorrecto de parámetros", en lugar de un error S0022 de SQLSTATE, "columna no encontrada".  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en un valor NULL. una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no se realizará correctamente en esa columna.
