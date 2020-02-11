---
title: Consulta y actualización de datos de Visual FoxPro desde Microsoft Access | Microsoft Docs
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
ms.openlocfilehash: 2681ecd0fe6f586954236c4fb5fddcf576b206be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988059"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Consultar y actualizar datos de Visual FoxPro desde Microsoft Access
Puede consultar y actualizar los datos almacenados en una base de datos de Visual FoxPro desde una base de datos de Microsoft Access mediante la opción vincular tabla.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Para vincular una base de datos de Visual FoxPro a una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En la pestaña tablas, haga clic en nuevo.  
  
3.  En el cuadro de diálogo Nueva tabla, seleccione vincular tabla y haga clic en Aceptar.  
  
4.  En el cuadro de diálogo vínculo, seleccione base de datos ODBC en la lista archivos de tipo.  
  
5.  En el cuadro de diálogo orígenes de datos SQL, seleccione el origen de datos que se conecta a los datos de Visual FoxPro que desea consultar y haga clic en Aceptar.  
  
6.  En el cuadro de diálogo vincular tablas, seleccione las tablas que desea consultar y actualizar y haga clic en Aceptar. Las tablas vinculadas de Visual FoxPro se muestran en la pestaña tablas de la base de datos de Microsoft Access.  
  
 Ahora puede usar Microsoft Access para consultar y actualizar los datos de las tablas de Visual FoxPro vinculadas. Los cambios que realice en los datos vinculados se devuelven al origen de datos de Visual FoxPro.  
  
 Si no desea que los cambios que realice en Microsoft Access afecten a los datos del origen de datos de Visual FoxPro, consulte [importación de datos de Visual FoxPro en Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
