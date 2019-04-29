---
title: Asigna explícitamente descriptores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049794"
---
# <a name="explicitly-allocated-descriptors"></a>Descriptores asignados explícitamente
Una aplicación puede asignar explícitamente un descriptor de aplicación en una conexión en cualquier momento en que está conectado a la base de datos. Mediante la especificación de ese identificador de descriptor como un atributo de una instrucción controlar mediante **SQLSetStmtAttr**, la aplicación dirige al controlador que use ese descriptor en lugar de la correspondiente asignado implícitamente la aplicación descriptores. La aplicación no puede especificar los descriptores de implementación alternativa.  
  
 Una aplicación puede asociar un descriptor asignado explícitamente a más de una instrucción. Solo cuando una aplicación está realmente conectada a la base de datos puede ser un descriptor de un descriptor asignado explícitamente. La aplicación puede liberar un descriptor de tal explícita o implícitamente al liberar la conexión.
