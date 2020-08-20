---
description: Descriptores asignados explícitamente
title: Descriptores asignados explícitamente | Microsoft Docs
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
ms.openlocfilehash: 7215d17a7156419f08bbd73528c468d7b6355b94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461487"
---
# <a name="explicitly-allocated-descriptors"></a>Descriptores asignados explícitamente
Una aplicación puede asignar explícitamente un descriptor de aplicación en una conexión en cualquier momento que esté conectado a la base de datos. Al especificar ese identificador de descriptor como un atributo de un identificador de instrucción mediante **SQLSetStmtAttr**, la aplicación indica al controlador que use ese descriptor en lugar de los descriptores de aplicación asignados implícitamente correspondientes. La aplicación no puede especificar descriptores de implementación alternativos.  
  
 Una aplicación puede asociar un descriptor asignado explícitamente a más de una instrucción. Solo cuando una aplicación está conectada realmente a la base de datos, puede que un descriptor sea un descriptor asignado explícitamente. La aplicación puede liberar este descriptor explícitamente o implícitamente liberando su conexión.
