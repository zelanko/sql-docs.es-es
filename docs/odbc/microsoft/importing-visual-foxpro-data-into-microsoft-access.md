---
title: Importar datos de Visual FoxPro en Microsoft Access | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bdf35fb9c9b7b4688aa7f5bf4173b2a6a9eefb5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar datos de Visual FoxPro en Microsoft Access
Puede importar los datos almacenados en una base de datos de Visual FoxPro en una base de datos de Microsoft Access mediante la opción Importar.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar datos de Visual FoxPro en una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En el menú archivo, elija que obtener datos externos, a continuación, importar.  
  
3.  En el cuadro de diálogo de importación, seleccione las bases de datos ODBC en los archivos de lista de tipos.  
  
4.  En el cuadro de diálogo orígenes de datos de SQL, seleccione el origen de datos de Visual FoxPro que se conecta a los datos de FoxPro que desea consultar y haga clic en Aceptar.  
  
5.  En el cuadro de diálogo Importar objetos, seleccione una o más tablas que desea importar y haga clic en Aceptar. Los nombres de las tablas de Visual FoxPro que importó se muestran en la ficha de tablas de la base de datos de Microsoft Access.  
  
 Ahora puede utilizar Microsoft Access para manipular los datos en las tablas de Visual FoxPro importadas. Los datos que importa están una instantánea de los datos almacenados en Visual FoxPro; no se envían los cambios realizados en los datos importados en el origen de datos de Visual FoxPro.  
  
 Si desea que los cambios realice en Microsoft Access para cambiar los datos en el origen de datos de Visual FoxPro, consulte [consultas y actualización de Visual FoxPro datos desde Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).

