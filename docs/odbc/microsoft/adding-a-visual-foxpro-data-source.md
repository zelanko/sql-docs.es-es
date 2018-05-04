---
title: Agregar un origen de datos de Visual FoxPro | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d59ad4b7663202b0ca66fc0eabb4ad6405760d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="adding-a-visual-foxpro-data-source"></a>Agregar un origen de datos de Visual FoxPro
Para obtener acceso a datos de Visual FoxPro desde su aplicación, debe tener un origen de datos. Puede crear un origen de datos como sigue:  
  
-   En una aplicación, como Microsoft® Word, Microsoft Excel o Microsoft Access, que usa controladores ODBC.  
  
-   Fuera de la aplicación, utilizando el Microsoft Windows® 95, Microsoft Windows 98 o Panel de Control de Microsoft Windows/Windows 2000.  
  
 Después de un origen de datos existe en el sistema, puede reutilizar el mismo origen de datos cada vez que se desea tener acceso a datos de Visual FoxPro. Si tiene varias bases de datos diferentes o tablas que desea tener acceso, puede crear un origen de datos independiente para cada base de datos o el directorio.  
  
 El procedimiento siguiente crea un origen de datos mediante el Panel de Control. Para obtener más información sobre cómo crear un origen de datos de una aplicación, consulte [acceso a Visual FoxPro datos desde Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Para agregar un origen de datos de Visual FoxPro  
  
1.  En equipos que ejecutan Windows 2000, abra el panel de Control de Windows y haga doble clic en Herramientas administrativas.  
  
2.  Haga doble clic en orígenes de datos (ODBC) para abrir el cuadro de diálogo Administrador de orígenes de datos ODBC. Este icono está disponible después de haber instalado el controlador ODBC de Visual FoxPro o cualquier software de controlador ODBC.  
  
    > [!NOTE]  
    >  Si se ejecuta una versión anterior de Windows, abra el panel de Control de Windows y haga doble clic en ODBC u ODBC de 32 bits para abrir el cuadro de diálogo Administrador de orígenes de datos ODBC.  
  
3.  Haga clic en Agregar.  
  
4.  En el cuadro de diálogo Crear nuevo origen de datos, seleccione Microsoft Visual FoxPro Driver y, a continuación, haga clic en Finalizar.  
  
5.  En el [cuadro de diálogo del programa de instalación de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), escriba el nombre del origen de datos y la descripción, seleccione el tipo de base de datos, seleccione la base de datos o el directorio y, a continuación, haga clic en Aceptar.  
  
     El nuevo nombre de origen de datos se muestra en la lista de orígenes de datos de usuario en la ficha DSN de usuario del cuadro de diálogo Administrador de orígenes de datos ODBC.  
  
6.  Haga clic en Aceptar para guardar el nuevo origen de datos y cerrar el cuadro de diálogo Administrador de orígenes de datos ODBC.
