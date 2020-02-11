---
title: Usar el controlador ODBC de VFP FoxPro con la aplicación Visual Basic | Microsoft Docs
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
ms.openlocfilehash: 017e8e7897b2b792d7a864dc336537d76dcad8b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087983"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Utiliza el controlador ODBC de Visual FoxPro con la aplicación de Visual Basic
Su aplicación Microsoft® Visual Basic® puede comunicarse con los datos de Visual FoxPro mediante la creación de un control de datos que se conecta a un origen de datos de Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para conectarse a los datos de Visual FoxPro mediante el control de datos en Visual Basic  
  
1.  Cree un origen de datos denominado "Test" que se conecte a la base de datos de ejemplo TasTrade que se incluye en Visual FoxPro. La instalación de Visual FoxPro predeterminada coloca la base de datos de ejemplo TasTrade en la ubicación:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  En Visual Basic, cree un nuevo formulario y coloque un cuadro de texto y un control de datos en él.  
  
3.  Cambie la propiedad Connect del control de datos como se indica a continuación:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Cambie la propiedad TipoRecordset por lo siguiente:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Cambie la propiedad OrigenDelRegistro por lo siguiente:  
  
    ```  
    customer  
    ```  
  
6.  Cambie la propiedad DataSource del cuadro de texto por el nombre predeterminado del control de datos por lo siguiente:  
  
    ```  
    data1  
    ```  
  
7.  Cambie la propiedad DataField del cuadro de texto a la siguiente:  
  
    ```  
    customer_id  
    ```  
  
8.  Ejecute el formulario y use el control de datos para omitir los campos de ID. de cliente de la base de datos de ejemplo TasTrade de Visual FoxPro.
