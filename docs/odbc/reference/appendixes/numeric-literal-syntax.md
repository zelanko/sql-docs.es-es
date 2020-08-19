---
description: Sintaxis de los literales numéricos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be87238f1663bcf9b12d40cb90521bb404a25af3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425017"
---
# <a name="numeric-literal-syntax"></a>Sintaxis de los literales numéricos
La siguiente sintaxis se utiliza para los literales numéricos en ODBC:  
  
 *Numeric-literal* :: = *signed-numeric-literal &#124; unsigned-Numeric-literal*  
  
 *signed-Numeric-literal* :: = [*signo*] *unsigned-literal-literal*  
  
 *unsigned-Numeric-literal* :: = *Exact-numeric-literal &#124; aproximada-Numeric-literal*  
  
 *Exact-Numeric-literal* :: = *unsigned-Integer* [*period*[*unsigned-Integer*]] *&#124;period sin signo-entero*  
  
 *Sign* :: = *plus-Sign &#124; signo menos*  
  
 *aproximado-Numeric-literal* :: = *mantisa E exponente*  
  
 *mantisa* :: = *Exact-Numeric-literal*  
  
 *exponente* :: = *signed-Integer*  
  
 *signed-Integer* :: = [*Sign*] *unsigned-Integer*  
  
 *unsigned-Integer* :: = *digit...*  
  
 *signo más* :: = *+*  
  
 signo *menos* :: =-  
  
 *digit* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *period* :: =.
