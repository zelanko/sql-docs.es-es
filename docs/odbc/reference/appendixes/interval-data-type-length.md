---
description: Longitud del tipo de datos de intervalo
title: Longitud del tipo de datos de intervalo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 589a13e0f0b2c6e6e42ade0f0dc32415556a0efc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483288"
---
# <a name="interval-data-type-length"></a>Longitud del tipo de datos de intervalo
Las reglas siguientes se usan para determinar la longitud de un tipo de datos de intervalo en caracteres. La longitud se expresa en número de caracteres. El número de bytes depende del juego de caracteres. La longitud incluye los siguientes valores agregados juntos:  
  
-   Dos caracteres para cada campo del intervalo que no es el campo inicial.  
  
-   En el campo inicial, el número de caracteres que es la precisión inicial expresa o implícita. Si no se especifica la precisión inicial, el valor predeterminado es 2.  
  
-   Un carácter para el separador entre los campos.  
  
-   Uno más la precisión de segundos expresa o implícita. Si no se especifica la precisión de segundos, el valor predeterminado es 6.  
  
 Los valores de longitud de columna específicos para cada tipo de datos de intervalo se incluyen en [el tamaño de columna](../../../odbc/reference/appendixes/column-size.md).
