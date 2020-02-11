---
title: Jet 4,0 utiliza la lista de palabras reservadas de SQL-92 cuando ExtendedAnsiSQL_Set | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68058794"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>Lista de palabras reservadas de Jet 4.0 utiliza SQL-92 cuando ExtendedAnsiSQL_Set
Cuando la marca ExtendedAnsiSQL está activada, jet 4,0 usa la lista de palabras reservadas SQL-92. Si intenta utilizar una palabra reservada SQL-92 como nombre de objeto sin comillas, se producirá un error de sintaxis. Cuando la marca ExtendedAnsiSQL está desactivada, las nuevas palabras reservadas se pueden usar como nombres de objeto como antes.
