---
title: Longitud de tipo de datos de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16d0590d3297b52891bf399822ce984674022583
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808935"
---
# <a name="interval-data-type-length"></a>Longitud del tipo de datos de intervalo
Las reglas siguientes se usan para determinar la longitud de un tipo de datos de intervalo de caracteres. Está expresado en número de caracteres. El número de bytes depende el juego de caracteres. La longitud incluye los siguientes valores que suman:  
  
-   Dos caracteres para cada campo en el intervalo que no es el campo inicial.  
  
-   Para el campo inicial, el número de caracteres que es la precisión inicial expresa o implícita. Si no se especifica la precisión inicial, el valor predeterminado es 2.  
  
-   Un carácter para el separador entre los campos.  
  
-   Uno más la precisión de segundos expresas o implícitas. Si no se especifica la precisión en segundos, el valor predeterminado es 6.  
  
 Valores de longitud de columna específicos para cada tipo de datos de intervalo se encuentran en [tamaño de la columna](../../../odbc/reference/appendixes/column-size.md).
