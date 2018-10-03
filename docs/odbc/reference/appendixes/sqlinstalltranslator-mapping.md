---
title: Asignación de SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9760bfad769e9508d58d1cd00f98376dbd13d877
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831393"
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC 2. *x* aplicación llama a **SQLInstallTranslator** a través de una aplicación ODBC 3 *.x* controlador, el Administrador de controladores asigna la llamada a **SQLInstallTranslatorEx**. No debe llamar una aplicación **SQLInstallTranslator** en ODBC 3 *.x* Administrador de controladores con el *lpszInfFile* argumento establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF que se usa en ODBC 2. *x* ya no se admite en ODBC 3 *.x*, incluso para compatibilidad con versiones anteriores.
