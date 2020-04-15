---
title: Adición de un origen de datos de Visual FoxPro ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307146"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Agregar un origen de datos de Visual FoxPro
Para tener acceso a los datos de Visual FoxPro desde la aplicación, debe tener un origen de datos. Puede crear un origen de datos de la siguiente manera:  
  
-   En una aplicación, como Microsoft® Word, Microsoft Excel o Microsoft Access, que usa controladores ODBC.  
  
-   Fuera de la aplicación, mediante el Panel de control de Microsoft Windows® 95, Microsoft Windows 98 o Microsoft Windows NT®/Windows 2000.  
  
 Después de que exista un origen de datos en el sistema, puede reutilizar el mismo origen de datos cada vez que desee tener acceso a los datos de Visual FoxPro. Si tiene varias bases de datos o tablas diferentes a las que desea tener acceso, puede crear un origen de datos independiente para cada base de datos o directorio.  
  
 El siguiente procedimiento crea un origen de datos mediante el Panel de control. Para obtener más información acerca de cómo crear un origen de datos a partir de una aplicación, vea Acceso a datos de [Visual FoxPro desde Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Para agregar un origen de datos de Visual FoxPro  
  
1.  En equipos que ejecutan Windows 2000, abra el panel de control de Windows y haga doble clic en Herramientas administrativas.  
  
2.  Haga doble clic en Orígenes de datos (ODBC) para abrir el cuadro de diálogo Administrador de orígenes de datos ODBC. Este icono está disponible después de haber instalado el controlador ODBC de Visual FoxPro o cualquier software de controlador ODBC.  
  
    > [!NOTE]  
    >  Si está ejecutando una versión anterior de Windows, abra el panel de control de Windows y haga doble clic en ODBC u ODBC de 32 bits para abrir el cuadro de diálogo Administrador de orígenes de datos ODBC.  
  
3.  Haga clic en Agregar.  
  
4.  En el cuadro de diálogo Crear nuevo origen de datos, seleccione Controlador de Microsoft Visual FoxPro y, a continuación, haga clic en Finalizar.  
  
5.  En el cuadro de diálogo Configuración de [ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), escriba el nombre y la descripción del origen de datos, seleccione el tipo de base de datos, seleccione la base de datos o el directorio y, a continuación, haga clic en Aceptar.  
  
     El nuevo nombre de origen de datos se muestra en la lista Orígenes de datos de usuario en la ficha DSN de usuario del cuadro de diálogo Administrador de orígenes de datos ODBC.  
  
6.  Haga clic en Aceptar para guardar el nuevo origen de datos y cerrar el cuadro de diálogo Administrador de orígenes de datos ODBC.
