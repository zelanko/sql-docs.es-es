---
description: Instrucciones DDL
title: Instrucciones DDL | Microsoft Docs
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
ms.openlocfilehash: 395abe3eed64f37c000ecff6f0b68a6e0cb1d076
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424737"
---
# <a name="ddl-statements"></a>Instrucciones DDL
Las instrucciones del lenguaje de definición de datos (DDL) varían enormemente entre DBMS. ODBC SQL define instrucciones para las operaciones de definición de datos más comunes: crear y quitar tablas, índices y vistas; modificar tablas; y conceder y revocar los privilegios. Todas las demás instrucciones DDL son específicas del origen de datos. Por lo tanto, las aplicaciones interoperables no pueden realizar algunas operaciones de definición de datos. En general, esto no es un problema, ya que estas operaciones tienden a ser específicas del DBMS y son más adecuadas para el software de administración de bases de datos propietario incluido con la mayoría de los DBMS o el programa de instalación incluido con el controlador.  
  
 Otro problema en la definición de datos es que los nombres de los tipos de datos varían enormemente entre DBMS. En lugar de definir nombres de tipos de datos estándar y forzar que los controladores los conviertan en nombres específicos de DBMS, **SQLGetTypeInfo** proporciona una manera para que las aplicaciones detecten los nombres de tipo de datos específicos del DBMS. Las aplicaciones interoperables deben usar estos nombres en instrucciones SQL para crear y modificar tablas; los nombres que aparecen en el [Apéndice C: gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)y los [tipos de datos Apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md)son solo ejemplos.
