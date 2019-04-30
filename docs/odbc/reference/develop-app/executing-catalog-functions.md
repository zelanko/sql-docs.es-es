---
title: Ejecutar funciones de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc53e265ffa25c5ec598187f62505f18436f1c69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248342"
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Debido a una función de catálogo, crea un conjunto de resultados, es equivalente a ejecutar cualquier instrucción SQL generadora de conjunto de resultados. De hecho, las funciones de catálogo a menudo se implementan al ejecutar instrucciones SQL predefinidas o llamar procedimientos predefinidos que se suministran con el controlador o DBMS. Casi todo lo que se aplica a instrucciones SQL que crean conjuntos de resultados también se aplica a funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, tal como limita el número de filas devueltas por una **seleccione** instrucción.  
  
 Para ejecutar una función de catálogo, una aplicación simplemente llama a la función.  
  
 Para obtener más información acerca de las funciones de catálogo, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
