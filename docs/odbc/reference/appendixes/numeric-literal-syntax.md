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
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990720"
---
# <a name="numeric-literal-syntax"></a>Sintaxis de los literales numéricos
Literales numéricos en ODBC, se usa la sintaxis siguiente:  
  
 *numeric-literal* ::= *signed-numeric-literal &#124; unsigned-numeric-literal*  
  
 *literal numérico firmado* :: = [*sesión*] *literal numérico sin signo*  
  
 *unsigned-numeric-literal* ::= *exact-numeric-literal &#124; approximate-numeric-literal*  
  
 *literal numérico exacto* :: = *entero sin signo* [*período*[*entero sin signo*]]  *&#124;período entero sin signo*  
  
 *inicio de sesión* :: = *signo &#124; signo menos*  
  
 *literal numérico aproximado* :: = *exponente mantisa E*  
  
 *mantissa* ::= *exact-numeric-literal*  
  
 *exponent* ::= *signed-integer*  
  
 *entero firmado* :: = [*sesión*] *entero sin signo*  
  
 *entero unsigned* :: = *dígitos...*  
  
 *signo* :: = *+*  
  
 *signo* :: = -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
