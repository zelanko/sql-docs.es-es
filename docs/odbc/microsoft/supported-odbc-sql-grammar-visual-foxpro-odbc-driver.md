---
title: Gramática de SQL de ODBC compatible (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f72548d0708a63f887f7d6da4d4f5988500f0eef
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304088"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Gramática de SQL de ODBC compatibles (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Microsoft Visual FoxPro admite lo siguiente:  
  
-   Todas las instrucciones y cláusulas SQL en la gramática mínima de SQL de ODBC  
  
-   Una instrucción SQL adicional de la gramática básica de SQL de ODBC  
  
 En la tabla siguiente se enumeran los elementos admitidos por el controlador mediante el nivel de gramática de SQL de ODBC.  
  
|Nivel|Elementos|Elemento|  
|-----------|--------------|----------|  
|Mínima|lenguaje de definición de datos (DDL)|CREATE TABLE y DROP TABLE|  
||lenguaje de manipulación de datos (DML)|SELECCIONAR, insertar, actualizar y eliminar|  
||Expresiones|Simple (por ejemplo, un>B + C)|  
||Tipos de datos|CHAR, VARCHAR o LONG VARCHAR|  
  
 Además de la gramática de SQL de ODBC admitida, el controlador ODBC de Visual FoxPro admite la sintaxis completa del lenguaje Visual FoxPro nativo para los siguientes comandos de Visual FoxPro:  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [ELIMINAR ETIQUETA](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
