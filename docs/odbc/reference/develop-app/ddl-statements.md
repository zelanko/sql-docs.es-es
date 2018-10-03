---
title: Instrucciones de DDL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14d9eb18a5c6c3cbd62cea0c668f3c53f8da48f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626683"
---
# <a name="ddl-statements"></a>Instrucciones DDL
Instrucciones de lenguaje de definición (DDL) de datos varían enormemente según DBMS. SQL de ODBC define las instrucciones para las operaciones más comunes de definición de datos: crear y quitar tablas, índices y vistas; modificar tablas; conceder y revocar los privilegios. Todas las demás instrucciones de DDL son específicos del origen de datos. Por lo tanto, las aplicaciones interoperables no pueden realizar algunas operaciones de definición de datos. En general, esto no supone un problema, porque estas operaciones tienden a ser muy específicos para DBMS y son más adecuadas izquierda para el software de administración de base de datos propietaria se incluye con la mayoría de los DBMS o el programa de instalación se incluye con el controlador.  
  
 Otro problema en la definición de datos es ese tipo de datos nombres varían enormemente según DBMS. En lugar de definir nombres de tipo de datos estándar y forzar que los controladores para convertirlas a nombres específicos de DBMS, **SQLGetTypeInfo** proporciona una manera para que las aplicaciones detectar los nombres de tipo de datos específicos para DBMS. Aplicaciones interoperables deben usar estos nombres en las instrucciones SQL para crear y modificar las tablas; los nombres que aparecen en [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), y [apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md), son solo ejemplos.
