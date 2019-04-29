---
title: Controladores de escritorio de la base de datos ODBC de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- Jet-based ODBC drivers [ODBC]
- ODBC desktop database drivers [ODBC], about desktop database drivers
- desktop database drivers [ODBC]
- Jet-based ODBC drivers [ODBC], about Jet-based ODBC drivers
- desktop database drivers [ODBC], about desktop database drivers
ms.assetid: 4e505c65-a8dd-4283-ae28-313d8a3aa046
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81cdf1738d35d89c35c34500900be79f7702f877
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63045957"
---
# <a name="microsoft-odbc-desktop-database-drivers"></a>Controladores de escritorio de la base de datos ODBC de Microsoft
ODBC es una API que usa el lenguaje de consulta estructurado (SQL) como el idioma de acceso de la base de datos. Puede tener acceso a una amplia variedad de sistemas de administración de bases de datos (DBMS) con el mismo código de origen ODBC que directamente se incorpora en el código fuente de la aplicación. Con los controladores de base de datos de Microsoft ODBC escritorio, un usuario de una aplicación habilitada para ODBC puede abrir, consulta y actualizar una base de datos de escritorio a través de la interfaz ODBC.  
  
 Los controladores de base de datos de escritorio de Microsoft ODBC son un conjunto de Microsoft basadas en Jet de controladores ODBC. Mientras que los controladores de base de datos de escritorio de Microsoft ODBC 2.0 incluye controladores de 16 bits y 32 bits, las versiones 3.0 y versiones posteriores incluyen solo los controladores de 32 bits que funcionan en Windows 95 o versiones posteriores, Windows NT Workstation o versión 4.0, Windows 2000 Professional o Windows 2000 Server Servidor. Estos controladores proporcionan acceso a los siguientes tipos de orígenes de datos:  
  
-   Microsoft Access  
  
-   Microsoft Excel  
  
-   Paradox  
  
-   dBASE  
  
-   Text  
  
 Consulte [Visual FoxPro ODBC Driver](../../odbc/microsoft/visual-foxpro-odbc-driver.md) para obtener documentación detallada sobre el controlador de ODBC de Microsoft Visual FoxPro®.  
  
> [!NOTE]  
>  Acceso a otros orígenes de datos, como Lotus 1-2-3, Microsoft Exchange y HTML, se habilita mediante los controladores instalables de ISAM (IISAM). Para obtener más información acerca de estos controladores, vea "Acceso a datos externos" en la *referencia del programador del motor de base de datos Jet de Microsoft*. Controladores de base de datos ODBC Desktop 4.0 no admiten formatos de datos Btrieve y EMS.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Arquitectura de controladores de escritorio de la base de datos](../../odbc/microsoft/desktop-database-drivers-architecture.md)  
  
-   [Historial de los controladores de escritorio de la base de datos](../../odbc/microsoft/history-of-the-desktop-database-drivers.md)  
  
-   [Servicios de soporte técnico](../../odbc/microsoft/product-support.md)  
  
-   [Implementación de controladores de escritorio de la base de datos](../../odbc/microsoft/implementing-desktop-database-drivers.md)  
  
-   [Consideraciones sobre la programación de controlador de Microsoft Access](../../odbc/microsoft/microsoft-access-driver-programming-considerations.md)  
  
-   [Consideraciones sobre la programación de controlador de Microsoft Excel](../../odbc/microsoft/microsoft-excel-driver-programming-considerations.md)  
  
-   [Consideraciones sobre la programación de controlador de Paradox](../../odbc/microsoft/paradox-driver-programming-considerations.md)  
  
-   [Consideraciones sobre la programación de controlador de dBASE](../../odbc/microsoft/dbase-driver-programming-considerations.md)  
  
-   [Consideraciones sobre la programación de controlador de archivo de texto](../../odbc/microsoft/text-file-driver-programming-considerations.md)  
  
-   [Gramática de SQL de ODBC compatibles adicionales](../../odbc/microsoft/additional-supported-odbc-sql-grammar.md)  
  
-   [Limitaciones](../../odbc/microsoft/limitations.md)  
  
-   [Errores de ODBC](../../odbc/microsoft/odbc-errors.md)  
  
-   [Funciones de la API de ODBC compatibles](../../odbc/microsoft/supported-odbc-api-functions.md)
