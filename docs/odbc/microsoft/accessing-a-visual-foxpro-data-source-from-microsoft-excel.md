---
title: Acceso a un origen de datos de Visual FoxPro desde Microsoft Excel Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], accessing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 2c143020-0403-4592-80e0-84229f3d40be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4afaeebb5b3a0d2430eafc6febf98f2fb9c16bf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302086"
---
# <a name="accessing-a-visual-foxpro-data-source-from-microsoft-excel"></a>Obtiene acceso a un origen de datos de Visual FoxPro desde Microsoft Excel
Si tiene Microsoft Query instalado, puede crear un origen de datos en Microsoft Excel que se conecte a los datos de Visual FoxPro.  
  
### <a name="to-access-visual-foxpro-data-from-microsoft-excel"></a>Para acceder a los datos de Visual FoxPro desde Microsoft Excel  
  
1.  Abra una hoja de cálculo de Microsoft Excel.  
  
2.  En el menú Data (Datos), elija Get External Data (Obtener datos externos). Se abre Microsoft Query.  
  
3.  En el cuadro de diálogo Seleccionar origen de datos, haga clic en Otro.  
  
4.  En el orígenes de datos ODBC cuadro de diálogo, haga clic en nuevo.  
  
5.  En el cuadro de diálogo Agregar origen de datos, seleccione Controlador de Microsoft Visual FoxPro en el cuadro de lista Controladores ODBC instalados y haga clic en Aceptar.  
  
6.  En el cuadro de diálogo Configuración de [ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), escriba el nombre del origen de datos, seleccione el tipo de base de datos, escriba la ruta de acceso a la base de datos o directorio y haga clic en Aceptar.  
  
     El nuevo nombre del origen de datos se muestra en el cuadro de texto Escriba origen de datos del cuadro de diálogo Orígenes de datos ODBC.  
  
7.  Haga clic en Aceptar.  
  
     El nuevo nombre del origen de datos se selecciona en el cuadro de texto Orígenes de datos disponibles del cuadro de diálogo Seleccionar origen de datos.  
  
8.  Haga clic en Usar.  
  
 Ahora puede agregar tablas a la consulta abierta. Para obtener más información acerca de cómo crear una consulta, vea Importar datos en Microsoft Excel desde una base de datos de [Visual FoxPro](../../odbc/microsoft/importing-data-into-microsoft-excel-from-a-visual-foxpro-database.md).
