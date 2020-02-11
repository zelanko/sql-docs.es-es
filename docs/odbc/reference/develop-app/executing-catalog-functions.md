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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901272"
---
# <a name="executing-catalog-functions"></a>Ejecutar funciones de catálogo
Dado que una función de catálogo crea un conjunto de resultados, equivale a ejecutar cualquier instrucción SQL que genera el conjunto de resultados. De hecho, las funciones de catálogo suelen implementarse mediante la ejecución de instrucciones SQL predefinidas o la llamada a procedimientos predefinidos que se incluyen con el controlador o DBMS. Casi todo lo que se aplica a las instrucciones SQL que crean conjuntos de resultados también se aplica a las funciones de catálogo. Por ejemplo, el atributo de instrucción SQL_ATTR_MAX_ROWS limita el número de filas devueltas por la función de catálogo, al igual que limita el número de filas devueltas por una instrucción **Select** .  
  
 Para ejecutar una función de catálogo, una aplicación simplemente llama a la función.  
  
 Para obtener más información sobre las funciones de catálogo, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).
