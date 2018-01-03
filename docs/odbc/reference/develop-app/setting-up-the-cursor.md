---
title: Configurar el Cursor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b442a732eb16b4047eabe9c507eb5cd5d2887a99
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="setting-up-the-cursor"></a>Cómo configurar el Cursor
La aplicación puede especificar el tipo de cursor antes de ejecutar una instrucción que crea un resultado de conjunto. Esto consigue con el atributo de instrucción SQL_ATTR_CURSOR_TYPE. Si la aplicación no especifica explícitamente un tipo, se utilizará un cursor de solo avance. Para obtener un cursor mixto, una aplicación especifica un cursor controlado por conjunto de claves, pero declara un tamaño de conjunto de claves menor que el tamaño del conjunto de lo resultados.  
  
 Para los cursores controlados por conjunto de claves y mixtos, la aplicación también puede especificar el tamaño del conjunto de claves. Esto consigue con el atributo de instrucción SQL_ATTR_KEYSET_SIZE. Si el tamaño del conjunto de claves se establece en 0, lo que es el valor predeterminado, el tamaño de conjunto de claves se establece en el tamaño del conjunto de resultados y se utiliza un cursor controlado por conjunto de claves. Después de que se ha abierto el cursor, se puede cambiar el tamaño del conjunto de claves.  
  
 La aplicación también puede establecer el tamaño del conjunto de filas; Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), anteriormente en esta sección.
