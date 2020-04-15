---
title: Sintaxis literal numérica ? Microsoft Docs
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
ms.openlocfilehash: e035e3ec53c5b5494c029d6840b9f5c836821209
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299865"
---
# <a name="numeric-literal-syntax"></a>Sintaxis de los literales numéricos
La sintaxis siguiente se utiliza para literales numéricos en ODBC:  
  
 *literal numérico* ::- *literal numérico-firmado &#124; unsigned-numeric-literal*  
  
 *literal-numérico firmado* :: [*signo*] *unsigned-numeric-literal*  
  
 *unsigned-numeric-literal* ::- *literal exacto-numérico &#124; literal aproximado-numérico*  
  
 *exact-numeric-literal* ::- *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *signo* :: *- signo más &#124; menos-signo*  
  
 *aproximado-numérico-literal* :: ' *mantissa E exponente*  
  
 *mantissa* ::- *literal exacto-numérico*  
  
 *exponente* :: - *entero firmado*  
  
 *signed-integer* ::- [*sign*] *unsigned-integer*  
  
 *unsigned-integer* ::- *digit...*  
  
 *signo de además* ::*+*  
  
 *signo menos* :: -  
  
 *dígito* :: 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* ::.
