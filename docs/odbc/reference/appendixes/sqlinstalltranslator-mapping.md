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
ms.openlocfilehash: 50bfa00f482110d3d0695ef249e8758b5db02c80
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792811"
---
# <a name="sqlinstalltranslator-mapping"></a>Asignación de SQLInstallTranslator
Cuando un ODBC *2.x* aplicación llama a **SQLInstallTranslator** a través de un ODBC *3.x* controlador, el Administrador de controladores asigna la llamada a  **SQLInstallTranslatorEx**. No debe llamar una aplicación **SQLInstallTranslator** en ODBC *3.x* Administrador de controladores con el *lpszInfFile* argumento establecido en un valor distinto de NULL. El SDK de ODBC. Archivo INF que se usa en ODBC *2.x* ya no se admite en ODBC *3.x*, incluso para compatibilidad con versiones anteriores.
