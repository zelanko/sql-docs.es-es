---
title: Consultar y actualizar datos de Visual FoxPro desde Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1097e03c414d919a606ffd21ae50ffddf51173b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316758"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar y actualizar datos de Visual FoxPro desde Microsoft Access
Puede consultar y actualizar los datos almacenados en una base de datos de Visual FoxPro desde una base de datos de Microsoft Access mediante la opción de tabla de vínculos.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular una base de datos de Visual FoxPro a una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En la pestaña de tablas, haga clic en nuevo.  
  
3.  En el cuadro de diálogo nueva tabla, seleccione la tabla de vínculos y haga clic en Aceptar.  
  
4.  En el cuadro de diálogo de vínculo, seleccione la base de datos ODBC en la lista Tipo de archivo.  
  
5.  En el cuadro de diálogo orígenes de datos SQL, seleccione el origen de datos que se conecta a los datos de Visual FoxPro que desea consultar y haga clic en Aceptar.  
  
6.  En el cuadro de diálogo Vincular tablas, seleccione las tablas que desea consultar y actualizar y haga clic en Aceptar. Las tablas vinculadas de Visual FoxPro se muestran en la pestaña de tablas de la base de datos de Microsoft Access.  
  
 Ahora puede usar Microsoft Access para consultar y actualizar datos en las tablas vinculadas de Visual FoxPro. Cambios en los datos vinculados se envían en el origen de datos de Visual FoxPro.  
  
 Si no desea que los cambios que realice en Microsoft Access afecta a los datos en el origen de datos de Visual FoxPro, consulte [importación de Visual FoxPro datos en Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
