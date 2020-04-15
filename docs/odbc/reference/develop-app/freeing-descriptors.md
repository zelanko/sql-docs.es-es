---
title: Descriptores de liberación ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305606"
---
# <a name="freeing-descriptors"></a>Descriptores de liberación
Los descriptores asignados explícitamente se pueden liberar explícitamente, llamando a **SQLFreeHandle** con *HandleType* de SQL_HANDLE_DESC o implícitamente, cuando se libera el identificador de conexión. Cuando se libera un descriptor asignado explícitamente, todos los identificadores de instrucción a los que se aplica el descriptor liberado se revierten automáticamente a los descriptores asignados implícitamente para ellos.  
  
 Los descriptores asignados implícitamente solo se pueden liberar llamando a **SQLDisconnect**, que quita las instrucciones o descriptores abiertos en la conexión, o llamando a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT liberar un identificador de instrucción y todos los descriptores asignados implícitamente asociados a la instrucción. Un descriptor asignado implícitamente no se puede liberar mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC.  
  
 Incluso cuando se libera, un descriptor asignado implícitamente sigue siendo válido y **SQLGetDescField** se puede llamar en sus campos.
