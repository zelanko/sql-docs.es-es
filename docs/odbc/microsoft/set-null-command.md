---
title: Comando NULL | Documentos de Microsoft
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
helpviewer_keywords: set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1050db2b6a50fc794626b6017bd26af05f458a8a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="set-null-command"></a>Comando NULL del conjunto
Determina cómo se admiten valores null por el SQL de ALTER TABLE - SQL, CREATE TABLE - e INSERT - comandos SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Valor predeterminado para el controlador; el valor predeterminado de Visual FoxPro es OFF). Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE permitirá admitir valores null. Puede invalidar la compatibilidad con valor null para las columnas de la tabla mediante la inclusión de la cláusula NOT NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL insertará valores null en las columnas que no se incluye en la instrucción INSERT - cláusula VALUE de SQL. INSERT - SQL insertará valores null solo en columnas que admiten valores null.  
  
 OFF  
 Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE no permita valores null. Puede designar la compatibilidad con valor null para las columnas en ALTER TABLE y CREATE TABLE al incluir la cláusula NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL, inserta valores en blanco en las columnas que no se incluye en la instrucción INSERT - cláusula VALUE de SQL.  
  
## <a name="remarks"></a>Comentarios  
 SET NULL afecta a los valores nulos solo cómo son compatibles con ALTER TABLE, CREATE TABLE e INSERT - SQL. Otros comandos no se ven afectados por SET NULL.  
  
## <a name="see-also"></a>Vea también  
 [Modificar tabla - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Crear tabla - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
