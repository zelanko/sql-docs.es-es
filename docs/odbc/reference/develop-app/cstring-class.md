---
title: Clase CString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f5752602de4848b35298fb4c4a6a1efdf6519dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042491"
---
# <a name="cstring-class"></a>Clase CString
Dado que los objetos de la **CString** clase en Microsoft® Visual C++® están firmados y argumentos de cadena en las funciones ODBC no están firmados, aplicaciones que pasan **CString** objetos a las funciones ODBC sin conversión de ellos recibirá advertencias del compilador.
