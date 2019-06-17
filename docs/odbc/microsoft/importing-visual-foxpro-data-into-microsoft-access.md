---
title: Importar datos de Visual FoxPro en Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f19b58ba93c94088c4cae19f1093d89c8decb843
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471306"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar datos de Visual FoxPro en Microsoft Access
Puede importar los datos almacenados en una base de datos de Visual FoxPro en una base de datos de Microsoft Access mediante la opción de importación.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar datos de Visual FoxPro en una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En el menú archivo, elija que obtener datos externos, a continuación, importar.  
  
3.  En el cuadro de diálogo de importación, seleccione las bases de datos ODBC en la lista Tipo de archivo.  
  
4.  En el cuadro de diálogo orígenes de datos SQL, seleccione el origen de datos de Visual FoxPro que se conecta a los datos de FoxPro que desea consultar y haga clic en Aceptar.  
  
5.  En el cuadro de diálogo Importar objetos, seleccione una o varias tablas que desea importar y haga clic en Aceptar. Se muestran los nombres de las tablas de Visual FoxPro que importó en la pestaña de tablas de la base de datos de Microsoft Access.  
  
 Ahora puede usar Microsoft Access para manipular los datos en las tablas importadas de Visual FoxPro. Los datos que importa están una instantánea de los datos almacenados en Visual FoxPro; no se envían los cambios en los datos importados en el origen de datos de Visual FoxPro.  
  
 Si desea que los cambios que realice en Microsoft Access para cambiar los datos en el origen de datos de Visual FoxPro, consulte [consulta y actualización de Visual FoxPro datos desde Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
