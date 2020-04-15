---
title: Importación de datos a Microsoft Excel desde una base de datos de Visual FoxPro Microsoft Docs
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
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287675"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar datos a Microsoft Excel desde una base de datos de Visual FoxPro
Puede importar datos de Visual FoxPro a su hoja de cálculo de Microsoft Excel si ha definido un origen de datos para él. Para obtener información sobre cómo crear un origen de datos de Visual FoxPro, consulte Acceso a un origen de [datos de Visual FoxPro desde Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar datos de Visual FoxPro en una hoja de cálculo de Microsoft Excel  
  
1.  Abra una hoja de cálculo de Microsoft Excel.  
  
2.  En el menú Data (Datos), elija Get External Data (Obtener datos externos). Se abre Microsoft Query.  
  
3.  En el cuadro de diálogo Seleccionar origen de datos, seleccione un origen de datos de Visual FoxPro y, a continuación, haga clic en Usar.  
  
4.  Si la base de datos a la que accede el origen de datos incluye tablas, seleccione una tabla en el cuadro de diálogo Agregar tablas. Microsoft Query muestra la tabla agregada en la mitad superior del diseñador de consultas.  
  
    > [!NOTE]  
    >  La lista Propietario no está disponible en este cuadro de diálogo porque el controlador no admite propietarios. La lista Base de datos no está disponible porque el controlador no admite varias bases de datos en un origen de datos.  
  
5.  Seleccione campos para la consulta arrastrándolos desde la tabla hasta la mitad inferior del diseñador.  
  
6.  Cierre Microsoft Query. Los datos seleccionados se importan a la hoja de cálculo de Microsoft Excel.
