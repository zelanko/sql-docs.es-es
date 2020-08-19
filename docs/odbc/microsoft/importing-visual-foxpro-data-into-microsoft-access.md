---
description: Importar datos de Visual FoxPro en Microsoft Access
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38440ca61b8af951f201978013d30529b75a452b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449537"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar datos de Visual FoxPro en Microsoft Access
Puede importar datos almacenados en una base de datos de Visual FoxPro en una base de datos de Microsoft Access mediante la opción de importación.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar datos de Visual FoxPro en una base de datos de Microsoft Access  
  
1.  Abra una base de datos de Microsoft Access.  
  
2.  En el menú Archivo, elija obtener datos externos y, a continuación, importar.  
  
3.  En el cuadro de diálogo Importar, seleccione bases de datos ODBC en la lista archivos de tipo.  
  
4.  En el cuadro de diálogo orígenes de datos SQL, seleccione el origen de datos de Visual FoxPro que se conecta a los datos de FoxPro que desea consultar y haga clic en Aceptar.  
  
5.  En el cuadro de diálogo Importar objetos, seleccione una o varias tablas que desee importar y haga clic en Aceptar. Los nombres de las tablas de Visual FoxPro que ha importado se muestran en la pestaña tablas de la base de datos de Microsoft Access.  
  
 Ahora puede usar Microsoft Access para manipular los datos de las tablas de Visual FoxPro importadas. Los datos que se importan son una instantánea de los datos almacenados en Visual FoxPro; los cambios que realice en los datos importados no se devolverán al origen de datos de Visual FoxPro.  
  
 Si desea que los cambios que realice en Microsoft Access cambien los datos en el origen de datos de Visual FoxPro, consulte [consultar y actualizar datos de Visual FoxPro desde Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
