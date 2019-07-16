---
title: Usar sinónimos con procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e798a9c7fa3365082a2e6dab562596d56649ec4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088022"
---
# <a name="using-synonyms-with-stored-procedures"></a>Usar sinónimos con procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para las versiones 2.0 y 2.5 de Oracle no admiten sinónimos cuando los procedimientos almacenados de Oracle que realiza la llamada. Sinónimos funcionan según lo esperado cuando se usa con otros objetos de base de datos de Oracle como tablas.
