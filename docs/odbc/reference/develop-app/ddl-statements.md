---
title: Declaraciones de DDL ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae06efe6dd11e651e8553fa5c1004c2fa145478
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302996"
---
# <a name="ddl-statements"></a>Instrucciones DDL
Las instrucciones de lenguaje de definición de datos (DDL) varían enormemente entre los DBMS. ODBC SQL define instrucciones para las operaciones de definición de datos más comunes: crear y quitar tablas, índices y vistas; alterar las tablas; y conceder y revocar privilegios. Todas las demás instrucciones DDL son específicas del origen de datos. Por lo tanto, las aplicaciones interoperables no pueden realizar algunas operaciones de definición de datos. En general, esto no es un problema, porque tales operaciones tienden a ser altamente específicas de DBMS y son mejor dejar al software de administración de bases de datos propietario suministrado con la mayoría de los DBMS o el programa de instalación incluido con el controlador.  
  
 Otro problema en la definición de datos es que los nombres de tipos de datos varían enormemente entre los DBMS. En lugar de definir nombres de tipos de datos estándar y forzar a los controladores para convertirlos en nombres específicos de DBMS, **SQLGetTypeInfo** proporciona una manera para que las aplicaciones detecten nombres de tipo de datos específicos de DBMS. Las aplicaciones interoperables deben usar estos nombres en instrucciones SQL para crear y modificar tablas; los nombres enumerados en [el Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)y Apéndice [D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos , son solo ejemplos.
