---
title: Admite la gramática de SQL de ODBC (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f899e8282dd4aaafe7f943acaa5ed1c82b8a93e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Gramática de SQL de ODBC compatibles (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Microsoft Visual FoxPro admite lo siguiente:  
  
-   Todas las instrucciones SQL y las cláusulas de la gramática mínima de SQL de ODBC  
  
-   Una instrucción SQL adicional desde el núcleo ODBC gramática de SQL  
  
 En la tabla siguiente se enumera los elementos compatibles con el controlador, por nivel de gramática de SQL de ODBC.  
  
|Nivel|Elementos|Elemento|  
|-----------|--------------|----------|  
|Mínima|lenguaje de definición de datos (DDL)|CREATE TABLE y DROP TABLE|  
||lenguaje de manipulación de datos (DML)|SELECT, INSERT, UPDATE y DELETE|  
||Expresiones|Simple (por ejemplo, A > B + C)|  
||Tipos de datos|CHAR, VARCHAR o LONG VARCHAR|  
  
 Además de la gramática de SQL de ODBC compatible, el controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo completa para los siguientes comandos de Visual FoxPro:  
  
 [MODIFICAR TABLA](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [ELIMINAR ETIQUETA](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
