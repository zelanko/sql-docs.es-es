---
title: Consultar y actualizar datos de Visual FoxPro desde Microsoft Access | Documentos de Microsoft
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
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eefdf130a261945a17c9ec557235b65ab7133fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar y actualizar datos de Visual FoxPro desde Microsoft Access
Puede consultar y actualizar los datos almacenados en una base de datos de Visual FoxPro desde una base de datos de Microsoft Access mediante la opción de tabla de vínculos.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular una base de datos de Visual FoxPro a una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En la ficha tablas, haga clic en nuevo.  
  
3.  En el cuadro de diálogo nueva tabla, seleccione la tabla de vínculos y haga clic en Aceptar.  
  
4.  En el cuadro de diálogo de vínculo, seleccione la base de datos de ODBC en la lista Tipo de archivo.  
  
5.  En el cuadro de diálogo orígenes de datos de SQL, seleccione el origen de datos que se conecta a los datos de Visual FoxPro que desea consultar y haga clic en Aceptar.  
  
6.  En el cuadro de diálogo Vincular tablas, seleccione las tablas que desea consultar y actualizar y haga clic en Aceptar. Las tablas de Visual FoxPro vinculadas se muestran en la ficha de tablas de la base de datos de Microsoft Access.  
  
 Ahora puede utilizar Microsoft Access para consultar y actualizar los datos de las tablas vinculadas de Visual FoxPro. Cambios realizados en los datos vinculados se envían en el origen de datos de Visual FoxPro.  
  
 Si no desea cambios realice en Microsoft Access afecta a los datos en el origen de datos de Visual FoxPro, consulte [importar Visual FoxPro datos en Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
