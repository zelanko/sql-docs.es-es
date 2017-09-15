---
title: Comando NULL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14cade223de7014dd4a0c27295d3ff742d18af17
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
