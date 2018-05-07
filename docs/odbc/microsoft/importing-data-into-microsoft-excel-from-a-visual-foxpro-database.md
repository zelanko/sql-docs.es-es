---
title: Importar datos a Microsoft Excel desde una base de datos de Visual FoxPro | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d3e7b1b915e27bb1f687631c68cbea2ef5d8fd8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar datos a Microsoft Excel desde una base de datos de Visual FoxPro
Puede importar datos de Visual FoxPro en la hoja de cálculo de Microsoft Excel si ha definido un origen de datos para él. Para obtener información acerca de cómo crear un origen de datos de Visual FoxPro, consulte [obtiene acceso a un origen de datos de Visual FoxPro desde Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar datos de Visual FoxPro en una hoja de cálculo de Microsoft Excel  
  
1.  Abra una hoja de cálculo de Microsoft Excel.  
  
2.  En el menú datos, elija obtener datos externos. Se abre Microsoft Query.  
  
3.  En el cuadro de diálogo Seleccionar origen de datos, seleccione un origen de datos de Visual FoxPro y, a continuación, haga clic en uso.  
  
4.  Si la base de datos tiene acceso a su origen de datos incluye tablas, seleccione una tabla en el cuadro de diálogo Agregar tablas. Microsoft Query muestra la tabla agregada en la mitad superior del Diseñador de consultas.  
  
    > [!NOTE]  
    >  La lista de propietario no está disponible en este cuadro de diálogo porque el controlador no es compatible con los propietarios. La lista de bases de datos no está disponible porque el controlador no admite varias bases de datos en un origen de datos.  
  
5.  Seleccionar campos para la consulta, arrástrelos desde la tabla menor será la mitad del diseñador.  
  
6.  Cierre Microsoft Query. Los datos seleccionados se importan en la hoja de cálculo de Microsoft Excel.
