---
title: Comando SET NULL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300815"
---
# <a name="set-null-command"></a>Comando NULL del conjunto
Determina cómo se admiten los valores NU con los comandos ALTER TABLE - SQL, CREATE TABLE - SQL e INSERT - SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTIVAR  
 (Predeterminado para el controlador; el valor predeterminado para Visual FoxPro es OFF.) Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE permitirán valores nulos. Puede invalidar la compatibilidad con valores NULL para las columnas de la tabla incluyendo la cláusula NOT NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL insertará valores NU en cualquier columna no incluida en la cláusula INSERT - SQL VALUE. INSERT: SQL insertará valores nulos solo en columnas que permitan valores nulos.  
  
 Apagado  
 Especifica que todas las columnas de una tabla creada con ALTER TABLE y CREATE TABLE no permitirán valores nulos. Puede designar la compatibilidad con valores nulos para las columnas de ALTER TABLE y CREATE TABLE incluyendo la cláusula NULL en las definiciones de las columnas.  
  
 También especifica que INSERT - SQL insertará valores en blanco en las columnas no incluidas en la cláusula INSERT - SQL VALUE.  
  
## <a name="remarks"></a>Observaciones  
 SET NULL solo afecta a cómo ALTER TABLE, CREATE TABLE e INSERT - SQL admiten valores nulos. SET NULL no afecta a otros comandos.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER TABLE - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [Insertar: comando SQL](../../odbc/microsoft/insert-sql-command.md)
