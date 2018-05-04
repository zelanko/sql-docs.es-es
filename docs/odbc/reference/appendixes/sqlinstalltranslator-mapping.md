---
title: Asignación de SQLInstallTranslator | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: 00fcaf15458873da56d1d37d2234fd14bf7bbbd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC 2. *x* aplicación llama **SQLInstallTranslator** a través de una aplicación ODBC 3 *.x* controlador, el Administrador de controladores asigna la llamada a **SQLInstallTranslatorEx**. Una aplicación no debe llamar a **SQLInstallTranslator** en ODBC 3 *.x* el Administrador de controladores con el *lpszInfFile* establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF utilizada en ODBC 2. *x* ya no se admite en ODBC 3 *.x*, ni siquiera para compatibilidad con versiones anteriores.
