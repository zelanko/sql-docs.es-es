---
title: Ejecutar funciones de catálogo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 854a7e7fe347bb02c59fe1608afd74bf87be6b7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Dado que una función de catálogo, crea un conjunto de resultados, equivale a ejecutar cualquier instrucción de SQL: Generar conjunto de resultados. De hecho, las funciones de catálogo se implementan a menudo ejecutando instrucciones SQL predefinidas o llamar a procedimientos predefinidos que se suministran con el controlador o el DBMS. Casi todo lo que se aplica a instrucciones SQL que crean conjuntos de resultados también se aplica a funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, tal y como limita el número de filas devueltas por una **seleccione** instrucción.  
  
 Para ejecutar una función de catálogo, una aplicación simplemente llama a la función.  
  
 Para obtener más información acerca de las funciones de catálogo, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
