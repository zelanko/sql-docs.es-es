---
description: Cómo configurar el Cursor
title: Configurar el cursor | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 307245dc403167f5bd857005f084ed22498d3ee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424587"
---
# <a name="setting-up-the-cursor"></a>Cómo configurar el Cursor
La aplicación puede especificar el tipo de cursor antes de ejecutar una instrucción que crea un conjunto de resultados. Lo hace con el atributo de instrucción SQL_ATTR_CURSOR_TYPE. Si la aplicación no especifica explícitamente un tipo, se usará un cursor de solo avance. Para obtener un cursor mixto, una aplicación especifica un cursor controlado por conjunto de claves, pero declara un tamaño de conjunto de claves menor que el tamaño del conjunto de resultados.  
  
 En el caso de los cursores mixtos y controlados por conjunto de claves, la aplicación también puede especificar el tamaño del conjunto de claves. Lo hace con el atributo de instrucción SQL_ATTR_KEYSET_SIZE. Si el tamaño del conjunto de claves se establece en 0, que es el valor predeterminado, el tamaño del conjunto de claves se establece en el tamaño del conjunto de resultados y se utiliza un cursor controlado por conjunto de claves. El tamaño del conjunto de claves se puede cambiar una vez abierto el cursor.  
  
 La aplicación también puede establecer el tamaño del conjunto de filas; para obtener más información, vea [usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md), anteriormente en esta sección.
