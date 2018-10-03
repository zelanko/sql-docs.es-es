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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654928"
---
# <a name="cstring-class"></a>Clase CString
Dado que los objetos de la **CString** clase en Microsoft® Visual C++® están firmados y argumentos de cadena en las funciones ODBC no están firmados, aplicaciones que pasan **CString** objetos a las funciones ODBC sin conversión de ellos recibirá advertencias del compilador.
