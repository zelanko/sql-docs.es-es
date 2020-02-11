---
title: Limitaciones de la instrucción CREATE TABLE | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096594"
---
# <a name="create-table-statement-limitations"></a>Crear tabla instrucción limitaciones
Cuando se utiliza Microsoft Access, Microsoft Excel o Paradoxdriver, y no se especifica la longitud de una columna de texto o binaria (o se especifica como 0), la longitud de la columna se establecerá en 255.  
  
 Cuando se utiliza el controlador dBASE y no se especifica la longitud de una columna de texto o binaria (o se especifica como 0), la longitud de la columna se establecerá en 254.  
  
 Se admite un máximo de 255 columnas.  
  
 Cuando se usa el controlador de Microsoft Excel en un origen de datos de MicrosoftExcel 5,0, 7,0 o 97, no se puede crear una hoja de cálculo con el mismo nombre que una hoja de cálculo que se quitó anteriormente. Cuando el controlador de Microsoft Excel se usa para tener acceso a una hoja de cálculo de la versión 5,0, 7,0 o 97, una instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo.  
  
 Cuando se usa el controlador de Paradox, no se pueden agregar columnas una vez que se ha definido un índice en una tabla. Si la primera columna de la lista de argumentos de una instrucción CREATE TABLE crea un índice, no se puede incluir una segunda columna en la lista de argumentos.
