---
title: Vistas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e2dd512ab529f1fb5d216f4a2e459cd601d40e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67943754"
---
# <a name="schema-views"></a>Vistas de esquema
Una aplicación puede recuperar información de metadatos del DBMS, ya sea mediante una llamada a funciones de catálogo de ODBC o mediante INFORMATION_SCHEMA vistas. Las vistas se definen mediante el estándar ANSI SQL-92.  
  
 Si el DBMS y el controlador lo admiten, las vistas de INFORMATION_SCHEMA proporcionan un medio más eficaz y completo para recuperar los metadatos de los que proporcionan las funciones del catálogo de ODBC. Una aplicación puede ejecutar su propia instrucción **Select** personalizada en una de estas vistas, puede combinar vistas o puede realizar una Unión en las vistas. A la vez que ofrece una mayor utilidad y una amplia gama de metadatos, las vistas INFORMATION_SCHEMA no suelen ser compatibles con el DBMS. Esto podría cambiar a medida que más DBMS y controladores logren el cumplimiento con SQL-92.  
  
 Para determinar qué vistas se admiten, una aplicación llama a **SQLGetInfo** con la opción SQL_INFO_SCHEMA_VIEWS. Para recuperar los metadatos de una vista compatible, la aplicación ejecuta una instrucción **Select** que especifica la información de esquema necesaria.
