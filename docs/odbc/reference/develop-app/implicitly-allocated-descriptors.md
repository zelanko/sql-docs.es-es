---
title: "Asigna implícitamente descriptores | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0746c31b05302eba9cd1fcf4104336ca139b6938
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="implicitly-allocated-descriptors"></a>Descriptores implícitamente asignados
Cuando se asigna un identificador de instrucción, la aplicación asigna implícitamente un conjunto de descriptores de cuatro. La aplicación puede obtener los identificadores de estos asigna implícitamente descriptores como atributos de identificador de instrucción. Cuando la aplicación libera el identificador de instrucción, el controlador libera todos los descriptores de implícitamente asignados en ese identificador.

