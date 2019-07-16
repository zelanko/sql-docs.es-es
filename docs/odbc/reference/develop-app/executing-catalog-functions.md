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
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901272"
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Debido a una función de catálogo, crea un conjunto de resultados, es equivalente a ejecutar cualquier instrucción SQL generadora de conjunto de resultados. De hecho, las funciones de catálogo a menudo se implementan al ejecutar instrucciones SQL predefinidas o llamar procedimientos predefinidos que se suministran con el controlador o DBMS. Casi todo lo que se aplica a instrucciones SQL que crean conjuntos de resultados también se aplica a funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, tal como limita el número de filas devueltas por una **seleccione** instrucción.  
  
 Para ejecutar una función de catálogo, una aplicación simplemente llama a la función.  
  
 Para obtener más información acerca de las funciones de catálogo, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
