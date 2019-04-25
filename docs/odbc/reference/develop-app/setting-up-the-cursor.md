---
title: Cómo configurar el Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445917"
---
# <a name="setting-up-the-cursor"></a>Cómo configurar el Cursor
La aplicación puede especificar el tipo de cursor antes de ejecutar una instrucción que crea un resultado de establece. Para hacerlo con el atributo de instrucción SQL_ATTR_CURSOR_TYPE. Si la aplicación no especifica explícitamente un tipo, se utilizará un cursor de solo avance. Para obtener un cursor mixto, una aplicación especifica un cursor dinámico, pero declara un conjunto de claves tamaño menor que el tamaño del conjunto de los resultados.  
  
 Para los cursores mixtos y dinámico, la aplicación también puede especificar el tamaño del conjunto de claves. Para hacerlo con el atributo de instrucción SQL_ATTR_KEYSET_SIZE. Si el tamaño del conjunto de claves se establece en 0, lo que es el valor predeterminado, el tamaño del conjunto de claves se establece en el tamaño del conjunto de resultados y se utiliza un cursor controlado por conjunto de claves. Después de que se ha abierto el cursor, se puede cambiar el tamaño del conjunto de claves.  
  
 La aplicación también puede establecer el tamaño del conjunto de filas. Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), anteriormente en esta sección.
