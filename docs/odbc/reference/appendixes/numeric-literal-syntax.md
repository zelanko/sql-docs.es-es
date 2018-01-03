---
title: "Sintaxis de los literales numéricos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 317b9753912c937399480473bca78bc7e11b7ce8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="numeric-literal-syntax"></a>Sintaxis de los literales numéricos
La siguiente sintaxis se utiliza para literales numéricos en ODBC:  
  
 *literal numérico* :: = *literal numérico firmado &#124; literal numérico sin signo*  
  
 *literal numérico firmado* :: = [*inicio de sesión*] *literal numérico sin signo*  
  
 *literal numérico sin signo* :: = *literal numérico exacto &#124; literales numéricos aproximados*  
  
 *literal numérico exacto* :: = *entero sin signo* [*período*[*entero sin signo*]] *&#124; período de entero sin signo*  
  
 *inicio de sesión* :: = *signos &#124; signo menos*  
  
 *literal numérico aproximado* :: = *exponente mantisa E*  
  
 *mantisa* :: = *literal numérico exacto*  
  
 *exponente* :: = *entero firmado*  
  
 *entero firmado* :: = [*inicio de sesión*] *entero sin signo*  
  
 *entero sin signo* :: = *dígitos...*  
  
 *signo* :: =*+*  
  
 *signo menos* :: = -  
  
 *dígitos* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período de* :: =.
