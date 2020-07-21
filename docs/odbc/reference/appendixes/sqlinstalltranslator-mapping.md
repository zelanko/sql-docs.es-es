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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300587"
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando una aplicación ODBC *2. x* llama a **SQLInstallTranslator** a través de un controlador ODBC *3. x* , el administrador de controladores asigna la llamada a **SQLInstallTranslatorEx**. Una aplicación no debe llamar a **SQLInstallTranslator** en el administrador de controladores ODBC *3. x* con el argumento *lpszInfFile* establecido en un valor distinto de NULL. El ODBC. El archivo INF que se usa en ODBC *2. x* ya no se admite en ODBC *3. x*, incluso para mantener la compatibilidad con versiones anteriores.
