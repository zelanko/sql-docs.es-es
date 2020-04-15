---
title: Consulta y actualización de datos de Visual FoxPro desde Microsoft Access Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11b49ed099ba29d0e7e013af99a8ad96ca6825c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292875"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar y actualizar datos de Visual FoxPro desde Microsoft Access
Puede consultar y actualizar los datos almacenados en una base de datos de Visual FoxPro desde una base de datos de Microsoft Access mediante la opción Tabla de vínculos.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular una base de datos de Visual FoxPro a una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En la pestaña Tablas, haga clic en Nuevo.  
  
3.  En el cuadro de diálogo Nueva tabla, seleccione Tabla de vínculos y haga clic en Aceptar.  
  
4.  En el cuadro de diálogo Vínculo, seleccione Base de datos ODBC en la lista Archivos de tipo.  
  
5.  En el cuadro de diálogo Orígenes de datos SQL, seleccione el origen de datos que se conecta a los datos de Visual FoxPro que desea consultar y haga clic en Aceptar.  
  
6.  En el cuadro de diálogo Tablas de vínculos, seleccione las tablas que desea consultar y actualizar y haga clic en Aceptar. Las tablas de Visual FoxPro vinculadas se muestran en la pestaña Tablas de la base de datos de Microsoft Access.  
  
 Ahora puede usar Microsoft Access para consultar y actualizar datos en las tablas de Visual FoxPro vinculadas. Los cambios realizados en los datos vinculados se devuelven al origen de datos de Visual FoxPro.  
  
 Si no desea que los cambios que realice en Microsoft Access afecten a los datos del origen de datos de Visual FoxPro, consulte Importación de datos de [Visual FoxPro en Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
