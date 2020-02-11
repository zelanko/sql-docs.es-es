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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069771"
---
# <a name="freeing-descriptors"></a>Descriptores de liberación
Los descriptores asignados explícitamente se pueden liberar explícitamente, llamando a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_DESC, o implícitamente, cuando se libera el identificador de conexión. Cuando se libera un descriptor asignado explícitamente, todos los identificadores de instrucción a los que se aplica el descriptor liberado se revierten automáticamente a los descriptores asignados implícitamente para ellos.  
  
 Los descriptores asignados implícitamente solo se pueden liberar llamando a **SQLDisconnect**, que quita todas las instrucciones o descriptores abiertas en la conexión, o bien llamando a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_STMT para liberar un identificador de instrucción y todos los descriptores asignados implícitamente asociados a la instrucción. Un descriptor asignado implícitamente no se puede liberar llamando a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC.  
  
 Incluso cuando se libera, un descriptor asignado implícitamente sigue siendo válido y se puede llamar a **SQLGetDescField** en sus campos.
