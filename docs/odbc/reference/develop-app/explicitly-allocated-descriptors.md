---
title: Descriptores explícitamente asignados (Explícitamente Asignados) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305696"
---
# <a name="explicitly-allocated-descriptors"></a>Descriptores asignados explícitamente
Una aplicación puede asignar explícitamente un descriptor de aplicación en una conexión en cualquier momento que esté conectada a la base de datos. Al especificar ese identificador de descriptor como un atributo de un identificador de instrucción mediante **SQLSetStmtAttr**, la aplicación indica al controlador que utilice ese descriptor en lugar de los descriptores de aplicación asignados implícitamente correspondientes. La aplicación no puede especificar descriptores de implementación alternativos.  
  
 Una aplicación puede asociar un descriptor asignado explícitamente a más de una instrucción. Solo cuando una aplicación está realmente conectada a la base de datos puede ser un descriptor asignado explícitamente. La aplicación puede liberar dicho descriptor explícitamente o implícitamente liberando su conexión.
