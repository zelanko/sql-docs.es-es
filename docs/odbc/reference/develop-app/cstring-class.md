---
title: La clase CString | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe6d7da568a104293d18712fe04fcca95dd360de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="cstring-class"></a>Clase CString
Porque los objetos de la **CString** clase en Microsoft® Visual C++® están firmados y argumentos de cadena de las funciones ODBC no están firmados, aplicaciones que pasan **CString** objetos a funciones ODBC sin conversión de ellos recibirá advertencias del compilador.
