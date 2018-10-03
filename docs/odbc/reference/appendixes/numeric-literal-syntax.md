---
title: Sintaxis de literales numéricos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18b1c144e84bf0be5aaeb68b66660f7bc7865ade
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601543"
---
# <a name="numeric-literal-syntax"></a>Sintaxis de los literales numéricos
Literales numéricos en ODBC, se usa la sintaxis siguiente:  
  
 *literal numérico* :: = *literal numérico firmado &#124; literal numérico sin signo*  
  
 *literal numérico firmado* :: = [*sesión*] *literal numérico sin signo*  
  
 *literal numérico sin signo* :: = *literal numérico exacto &#124; literal numérico aproximado*  
  
 *literal numérico exacto* :: = *entero sin signo* [*período*[*entero sin signo*]]  *&#124;período entero sin signo*  
  
 *inicio de sesión* :: = *signo &#124; signo menos*  
  
 *literal numérico aproximado* :: = *exponente mantisa E*  
  
 *mantisa* :: = *literal numérico exacto*  
  
 *exponente* :: = *entero firmado*  
  
 *entero firmado* :: = [*sesión*] *entero sin signo*  
  
 *entero unsigned* :: = *dígitos...*  
  
 *signo* :: = *+*  
  
 *signo* :: = -  
  
 *dígito* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
