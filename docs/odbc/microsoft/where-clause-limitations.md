---
description: DONDE cláusula limitaciones
title: Limitaciones de la cláusula WHERE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b6b9e72176f447c71daccfbd0393f414558d49d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466287"
---
# <a name="where-clause-limitations"></a>DONDE cláusula limitaciones
El número máximo de cláusulas en una cláusula WHERE es 40.  
  
 Las columnas LONGVARBINARY y LONGVARCHAR se pueden comparar con literales de hasta 255 caracteres de longitud, pero no se pueden comparar mediante parámetros.
