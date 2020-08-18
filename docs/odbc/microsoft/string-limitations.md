---
description: Limitaciones de cadena
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c21d86a3c626ced52c6b7915d3cfbd9322fb596e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449137"
---
# <a name="string-limitations"></a>Limitaciones de cadena
La longitud máxima de una cadena de instrucción SQL es de 65.000 caracteres.  
  
 Cuando se usa el controlador de Microsoft Access, solo se admiten las constantes de cadena de SQL-92 (con comillas simples, no comillas dobles).  
  
 El carácter de barra vertical (&#124;) no se puede usar en una cadena, tanto si el carácter está entre comillas como si no.  
  
 Para obtener la máxima interoperabilidad, las aplicaciones deben pasar cadenas en parámetros, en lugar de pasar cadenas entre comillas.
