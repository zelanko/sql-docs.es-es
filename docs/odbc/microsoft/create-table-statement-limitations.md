---
title: Crear tabla instrucción limitaciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db5d2cb8decde9828acd3005551717ac9f6cef32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096594"
---
# <a name="create-table-statement-limitations"></a>Crear tabla instrucción limitaciones
Cuando se usa el Microsoft Access, Microsoft Excel o Paradoxdriver y la longitud de una columna de texto o binario no se ha especificado (o se especifica como 0), se establecerá la longitud de columna en 255.  
  
 Cuando se usa el controlador de dBASE y la longitud de una columna de texto o binario no se ha especificado (o se especifica como 0), la longitud de columna se establecerá en 254.  
  
 Se admite un máximo de 255 columnas.  
  
 Cuando se usa el controlador de Microsoft Excel en un origen de 97 datos, una hoja de cálculo o en los 5.0, 7.0, no se puede crear con el mismo nombre que una hoja de cálculo que se ha quitado previamente. Cuando el controlador de Microsoft Excel se utiliza para tener acceso a una hoja de cálculo de la versión 5.0, 7.0 ó 97, una instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo.  
  
 Cuando se usa el controlador de Paradox, no se puede agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, una segunda columna no puede incluirse en la lista de argumentos.
