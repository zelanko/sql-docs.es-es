---
title: "Ejecutar funciones de catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f28435f84684037a8e796d7156605e4a0ed99476
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Dado que una función de catálogo, crea un conjunto de resultados, equivale a ejecutar cualquier instrucción de SQL: Generar conjunto de resultados. De hecho, las funciones de catálogo se implementan a menudo ejecutando instrucciones SQL predefinidas o llamar a procedimientos predefinidos que se suministran con el controlador o el DBMS. Casi todo lo que se aplica a instrucciones SQL que crean conjuntos de resultados también se aplica a funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, tal y como limita el número de filas devueltas por una **seleccione** instrucción.  
  
 Para ejecutar una función de catálogo, una aplicación simplemente llama a la función.  
  
 Para obtener más información acerca de las funciones de catálogo, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
