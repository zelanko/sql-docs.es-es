---
title: Marcadores de parámetros en las llamadas a procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1a0099e298b0326b5ccc19d6281fa3a091d57a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282505"
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parámetros en las llamadas a procedimiento
Cuando se llama a procedimientos que aceptan parámetros, las aplicaciones interoperables deben usar marcadores de parámetros en lugar de valores de parámetro literales. Algunos orígenes de datos no admiten el uso de valores de parámetros literales en llamadas a procedimientos. Para obtener más información sobre los parámetros, vea parámetros de la [instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre los procedimientos de llamada, vea [llamadas a](../../../odbc/reference/develop-app/procedure-calls.md)procedimientos, más adelante en esta sección.
