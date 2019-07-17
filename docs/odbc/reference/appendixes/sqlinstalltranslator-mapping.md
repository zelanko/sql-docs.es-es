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
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125729"
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC *2.x* aplicación llama a **SQLInstallTranslator** a través de un ODBC *3.x* controlador, el Administrador de controladores asigna la llamada a  **SQLInstallTranslatorEx**. No debe llamar una aplicación **SQLInstallTranslator** en ODBC *3.x* Administrador de controladores con el *lpszInfFile* argumento establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF que se usa en ODBC *2.x* ya no se admite en ODBC *3.x*, incluso para compatibilidad con versiones anteriores.
