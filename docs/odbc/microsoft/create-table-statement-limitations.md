---
title: "Crear tabla instrucción limitaciones | Documentos de Microsoft"
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
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d8f73082a87978bf735e2e44f97987ba34ffbb5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="create-table-statement-limitations"></a>Crear tabla instrucción limitaciones
Cuando se usa el Microsoft Access, Microsoft Excel o Paradoxdriver y la longitud de una columna de texto o binarios no se ha especificado (o se especifica como 0), la longitud de la columna se establecerá en 255.  
  
 Cuando se utiliza el controlador dBASE y la longitud de una columna de texto o binarios no se ha especificado (o se especifica como 0), la longitud de la columna se establecerá a 254.  
  
 Se admite un máximo de 255 columnas.  
  
 Cuando se usa el controlador de Microsoft Excel en un origen de 97 datos, una hoja de cálculo o en los 5.0, 7.0, no se puede crear con el mismo nombre que una hoja de cálculo que previamente se ha quitado. Cuando se usa el controlador de Microsoft Excel para tener acceso a una hoja de cálculo de la versión 5.0, 7.0 ó 97, una instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo.  
  
 Cuando se utiliza el controlador de Paradox, no se pueden agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, una segunda columna no puede incluirse en la lista de argumentos.
