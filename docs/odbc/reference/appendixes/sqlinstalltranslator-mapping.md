---
title: Asignación de SQLInstallTranslator | Documentos de Microsoft
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
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5de97b141f7ea2d1e3acf828f7d1b25bd77e0de7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC 2. *x* aplicación llama **SQLInstallTranslator** a través de una aplicación ODBC 3 *.x* controlador, el Administrador de controladores asigna la llamada a **SQLInstallTranslatorEx**. Una aplicación no debe llamar a **SQLInstallTranslator** en ODBC 3 *.x* el Administrador de controladores con el *lpszInfFile* establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF utilizada en ODBC 2. *x* ya no se admite en ODBC 3 *.x*, ni siquiera para compatibilidad con versiones anteriores.
