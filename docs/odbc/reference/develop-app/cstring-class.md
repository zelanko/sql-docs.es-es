---
title: La clase CString | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e3d3f3719fbc16a72f692b809eb646e7bbcf24d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="cstring-class"></a>Clase CString
Porque los objetos de la **CString** clase en Microsoft® Visual C++® están firmados y argumentos de cadena de las funciones ODBC no están firmados, aplicaciones que pasan **CString** objetos a funciones ODBC sin conversión de ellos recibirá advertencias del compilador.
