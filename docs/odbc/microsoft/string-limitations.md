---
title: Limitaciones de las cadenas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948763"
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es de 65.000 caracteres.  
  
 Cuando se usa el controlador de Microsoft Access, solo se admiten las constantes de cadena de SQL-92 (con comillas simples, no comillas dobles).  
  
 El carácter de barra vertical (&#124;) no se puede usar en una cadena, tanto si el carácter está entre comillas como si no.  
  
 Para obtener la máxima interoperabilidad, las aplicaciones deben pasar cadenas en parámetros, en lugar de pasar cadenas entre comillas.
