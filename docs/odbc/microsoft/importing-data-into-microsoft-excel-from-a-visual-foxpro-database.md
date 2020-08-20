---
description: Importar datos a Microsoft Excel desde una base de datos de Visual FoxPro
title: Importar datos en Microsoft Excel desde una base de datos de Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a4bd1cf7983ed0a552de4f9d0f491960b48f0d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500298"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar datos a Microsoft Excel desde una base de datos de Visual FoxPro
Puede importar datos de Visual FoxPro en la hoja de cálculo de Microsoft Excel si ha definido un origen de datos para él. Para obtener información acerca de la creación de un origen de datos de Visual FoxPro, vea [obtener acceso a un origen de datos de Visual FoxPro desde Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar datos de Visual FoxPro en una hoja de cálculo de Microsoft Excel  
  
1.  Abra una hoja de cálculo de Microsoft Excel.  
  
2.  En el menú datos, elija obtener datos externos. Se abre Microsoft Query.  
  
3.  En el cuadro de diálogo Seleccionar origen de datos, seleccione un origen de datos de Visual FoxPro y, a continuación, haga clic en usar.  
  
4.  Si la base de datos a la que tiene acceso el origen de datos incluye tablas, seleccione una tabla en el cuadro de diálogo Agregar tablas. Microsoft Query muestra la tabla agregada en la mitad superior del diseñador de consultas.  
  
    > [!NOTE]  
    >  La lista propietario no está disponible en este cuadro de diálogo porque el controlador no admite propietarios. La lista de bases de datos no está disponible porque el controlador no admite varias bases de datos en un origen de datos.  
  
5.  Seleccione los campos de la consulta arrastrándolos desde la tabla hasta la mitad inferior del diseñador.  
  
6.  Cierre Microsoft Query. Los datos seleccionados se importan en la hoja de cálculo de Microsoft Excel.
