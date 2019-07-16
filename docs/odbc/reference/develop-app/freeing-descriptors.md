---
title: Descriptores de liberación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069771"
---
# <a name="freeing-descriptors"></a>Descriptores de liberación
Descriptores asignados explícitamente pueden ser cualquiera liberar explícitamente, mediante una llamada a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_DESC o implícita, cuando se libera el identificador de conexión. Cuando se libera un descriptor asignado explícitamente, todos los identificadores de instrucciones a la que el descriptor liberado aplicado automáticamente volver a los descriptores implícitamente asignados para ellos.  
  
 Se pueden liberar los descriptores implícitamente asignados solo mediante una llamada a **SQLDisconnect**, que quita cualquier instrucción o descriptores de abrir en la conexión, o mediante una llamada a **SQLFreeHandle** con un  *HandleType* de SQL_HANDLE_STMT para liberar un identificador de instrucción y todos los descriptores implícitamente asignados asociados con la instrucción. No se puede liberar un descriptor asignado implícitamente mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC.  
  
 Incluso cuando se libera, un descriptor asignado implícitamente sigue siendo válido, y **SQLGetDescField** puede llamarse en sus campos.
