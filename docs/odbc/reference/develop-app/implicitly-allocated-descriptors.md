---
title: Asigna implícitamente descriptores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d805b110453c5fe0bb5be8c8df067c09ff8146e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="implicitly-allocated-descriptors"></a>Descriptores implícitamente asignados
Cuando se asigna un identificador de instrucción, la aplicación asigna implícitamente un conjunto de descriptores de cuatro. La aplicación puede obtener los identificadores de estos asigna implícitamente descriptores como atributos de identificador de instrucción. Cuando la aplicación libera el identificador de instrucción, el controlador libera todos los descriptores de implícitamente asignados en ese identificador.
