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
manager: craigg
ms.openlocfilehash: cf56bcc674299fd576529929da10763c26a74ed4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259537"
---
# <a name="using-synonyms-with-stored-procedures"></a>Usar sinónimos con procedimientos almacenados
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft para las versiones 2.0 y 2.5 de Oracle no admiten sinónimos cuando los procedimientos almacenados de Oracle que realiza la llamada. Sinónimos funcionan según lo esperado cuando se usa con otros objetos de base de datos de Oracle como tablas.
