---
title: Comando NULL del conjunto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6f0e23abd31661210282967fa35080376eaaaf3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159304"
---
# <a name="set-null-command"></a>Comando NULL del conjunto
Determina cómo se admiten valores null ALTER TABLE - SQL, CREATE TABLE - SQL, así como insertar - comandos SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Valor predeterminado para el controlador; el valor predeterminado de Visual FoxPro es OFF). Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE permitirá admitir valores null. Puede invalidar la compatibilidad con valor null para las columnas de la tabla mediante la inclusión de la cláusula NOT NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL insertará valores null en las columnas que no se incluye en la instrucción INSERT - cláusula SQL VALUE. INSERT - SQL insertará valores null solo en las columnas que permiten valores null.  
  
 OFF  
 Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE no permite valores null. Puede designar la compatibilidad con valor null para las columnas en ALTER TABLE y CREATE TABLE al incluir la cláusula NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL insertará los valores en blanco en las columnas que no se incluye en la instrucción INSERT - cláusula SQL VALUE.  
  
## <a name="remarks"></a>Comentarios  
 Se admiten los valores nulos solo cómo afecta a SET NULL mediante ALTER TABLE, CREATE TABLE e INSERT - SQL. Otros comandos no se ven afectados por SET NULL.  
  
## <a name="see-also"></a>Vea también  
 [Modificar tabla - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Crear tabla - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
