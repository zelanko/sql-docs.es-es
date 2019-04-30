---
title: Utilice el controlador ODBC de VFP FoxPro con la aplicación de Visual Basic | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b77fdee70ff73772710c9758eeb2bf2594f365d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280949"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Utiliza el controlador ODBC de Visual FoxPro con la aplicación de Visual Basic
Aplicación de Microsoft® Visual Basic® puede comunicarse con los datos de Visual FoxPro mediante la creación de un control de datos que se conecta a un origen de datos de Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para conectarse a datos de Visual FoxPro con el Control de datos en Visual Basic  
  
1.  Crear un origen de datos denominado "test" que se conecta a la base de datos de ejemplo TasTrade incluido en Visual FoxPro. La instalación de Visual FoxPro predeterminada coloca la base de datos de ejemplo TasTrade en la ubicación:  
  
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
  
5.  Cambie la propiedad de origen de registros a lo siguiente:  
  
    ```  
    customer  
    ```  
  
6.  Cambie la propiedad de origen de datos para el cuadro de texto en el nombre predeterminado para el control de datos a la siguiente:  
  
    ```  
    data1  
    ```  
  
7.  Cambie la propiedad DataField del cuadro de texto a lo siguiente:  
  
    ```  
    customer_id  
    ```  
  
8.  Ejecutar el formulario y usar el control de datos que se omiten a través de los campos de Id. de cliente de la base de datos de ejemplo TasTrade de Visual FoxPro.
