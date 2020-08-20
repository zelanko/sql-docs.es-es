---
description: Caso de identificador
title: Caso de identificador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ccac9b10e6a32c7265cd5f591944735454b85f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461453"
---
# <a name="identifier-case"></a>Caso de identificador
En las instrucciones SQL y los argumentos de la función de catálogo, los identificadores e identificadores entre comillas pueden distinguir entre mayúsculas y minúsculas, que una aplicación puede determinar llamando a **SQLGetInfo** con las opciones SQL_IDENTIFIER_CASE y SQL_QUOTED_IDENTIFIER_CASE.  
  
 Cada una de estas opciones tiene cuatro valores devueltos posibles: uno que indica que el identificador o el caso del identificador entre comillas es sensible y tres que indican que no es sensible. Los tres valores que no distinguen mayúsculas de minúsculas describen en detalle el caso en el que los identificadores se almacenan en el catálogo del sistema. La forma en que se almacenan los identificadores en el catálogo del sistema solo es relevante para la visualización, por ejemplo, cuando una aplicación muestra los resultados de una función de catálogo. no cambia la distinción de mayúsculas y minúsculas de los identificadores.
