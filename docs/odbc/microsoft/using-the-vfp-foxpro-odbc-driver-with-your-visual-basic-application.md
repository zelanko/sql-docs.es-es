---
title: Utilice el controlador ODBC de FoxPro VFP con la aplicación de Visual Basic | Documentos de Microsoft
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
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96107d42ae4923cd1b9f7ad1c16bd492d0203c99
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Utiliza el controlador ODBC de FoxPro VFP con la aplicación de Visual Basic
Aplicación de su Microsoft® Visual Basic® puede comunicarse con los datos de Visual FoxPro mediante la creación de un control de datos que se conecta a un origen de datos de Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para conectarse a datos de Visual FoxPro mediante el Control de datos en Visual Basic  
  
1.  Crear un origen de datos denominado "test" que se conecta a la base de datos de ejemplo de TasTrade incluido en Visual FoxPro. La instalación predeterminada de Visual FoxPro coloca la base de datos de ejemplo de TasTrade en la ubicación:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  En Visual Basic, cree un nuevo formulario y coloque un cuadro de texto y un control de datos en él.  
  
3.  Cambie la propiedad de conexión del control de datos como sigue:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Cambie la propiedad RecordsetType a lo siguiente:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Cambie la propiedad de origen de registros a la siguiente:  
  
    ```  
    customer  
    ```  
  
6.  Cambie la propiedad de origen de datos para el cuadro de texto para el nombre predeterminado para el control de datos a lo siguiente:  
  
    ```  
    data1  
    ```  
  
7.  Cambiar propiedades de DataField del cuadro de texto a lo siguiente:  
  
    ```  
    customer_id  
    ```  
  
8.  Ejecute el formulario y use el control de datos que se omiten a través de los campos de Id. de cliente de la base de datos de ejemplo TasTrade de Visual FoxPro.
