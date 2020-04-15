---
title: Vistas de esquema ( Schema Views) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304256"
---
# <a name="schema-views"></a>Vistas de esquema
Una aplicación puede recuperar información de metadatos del DBMS llamando a funciones de catálogo ODBC o mediante vistas de INFORMATION_SCHEMA. Las vistas se definen mediante el estándar ANSI SQL-92.  
  
 Si es compatible con el DBMS y el controlador, las vistas INFORMATION_SCHEMA proporcionan un medio más eficaz y completo de recuperar metadatos que las funciones de catálogo ODBC. Una aplicación puede ejecutar su propia instrucción **SELECT** personalizada en una de estas vistas, puede unir vistas o puede realizar una unión en vistas. Aunque ofrece una mayor utilidad y una gama más amplia de metadatos, el DBMS no admite a menudo INFORMATION_SCHEMA vistas. Esto podría cambiar a medida que más DBMS y controladores logran el cumplimiento de SQL-92.  
  
 Para determinar qué vistas se admiten, una aplicación llama a **SQLGetInfo** con la opción SQL_INFO_SCHEMA_VIEWS. Para recuperar metadatos de una vista admitida, la aplicación ejecuta una instrucción **SELECT** que especifica la información de esquema necesaria.
