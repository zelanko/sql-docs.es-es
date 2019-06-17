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
manager: craigg
ms.openlocfilehash: 782dec08b76a9e5a97719d6af39e2c30c0f92d19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468622"
---
# <a name="schema-views"></a>Vistas de esquema
Una aplicación puede recuperar información de metadatos de DBMS mediante una llamada a funciones de catálogo ODBC o mediante el uso de las vistas INFORMATION_SCHEMA. Las vistas se definen mediante el estándar ANSI SQL-92.  
  
 Si admite el controlador y el DBMS, las vistas INFORMATION_SCHEMA proporcionan un medio más eficaz y completa de recuperación de metadatos que proporcionan las funciones de catálogo ODBC. Una aplicación puede ejecutar su propio custom **seleccione** instrucción en una de estas vistas, puede unir las vistas, o puede realizar una unión en las vistas. Al tiempo que ofrece una gama más amplia de los metadatos y de mayor utilidad, vistas INFORMATION_SCHEMA no se admiten a menudo el DBMS. Esto podría cambiar como más DBMS y los controladores de lograr el cumplimiento con SQL-92.  
  
 Para determinar qué vistas se admiten, una aplicación llama a **SQLGetInfo** con la opción SQL_INFO_SCHEMA_VIEWS. Para recuperar los metadatos de una vista compatible, la aplicación ejecuta un **seleccione** instrucción que especifica la información de esquema necesaria.
