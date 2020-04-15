---
title: Ejecución de funciones de catálogo (Ejecución de funciones de catálogo) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305726"
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Dado que una función de catálogo crea un conjunto de resultados, equivale a ejecutar cualquier instrucción SQL de generación de conjuntos de resultados. De hecho, las funciones de catálogo a menudo se implementan mediante la ejecución de instrucciones SQL predefinidas o la llamada a procedimientos predefinidos que se incluyen con el controlador o DBMS. Casi todo lo que se aplica a instrucciones SQL que crean conjuntos de resultados también se aplica a las funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, del mismo modo que limita el número de filas devueltas por una instrucción **SELECT.**  
  
 Para ejecutar una función de catálogo, una aplicación solo llama a la función.  
  
 Para obtener más información acerca de las funciones de catálogo, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .
