---
title: Limitaciones de la instrucción SELECT | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 00490256cb4da90fc9384f696435419266a1a3d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900670"
---
# <a name="select-statement-limitations"></a>Limitaciones de la instrucción SELECT
No se pueden mezclar una columna de la función de agregado con una columna no agregado en una instrucción SELECT.  
  
 La lista de selección de una instrucción SELECT que contiene una cláusula GROUP BY solo puede tener expresiones de la cláusula GROUP BY o funciones de conjunto.  
  
 No se admite el uso de un asterisco (para seleccionar todas las columnas) en una instrucción SELECT que contiene una cláusula GROUP BY. Deben especificarse los nombres de las columnas que desea seleccionar.  
  
 No se admite el uso de una barra vertical en una instrucción SELECT. Usar un parámetro en la instrucción SELECT si tiene que hacer referencia a un valor de datos que contiene una barra vertical.  
  
 Al utilizar un alias de columna en una instrucción SELECT, la palabra "as" debe preceder a lo alias. Por ejemplo, "SELECT col1 como un de b." Sin el "como" la instrucción devolverá un error.  
  
 Si se especifica un nombre de columna incorrecto en una instrucción SELECT, se devuelve un error de SQLSTATE 07001, "Número de parámetros incorrectos," en lugar de un error de SQLSTATE S0022, "columna no encontrada."  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en un valor NULL; una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no surtirán efecto en esa columna.
