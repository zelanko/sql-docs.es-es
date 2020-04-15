---
title: Utilice el controlador ODBC de VFP FoxPro con la aplicación de Visual Basic . Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292705"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Utiliza el controlador ODBC de Visual FoxPro con la aplicación de Visual Basic
La aplicación Microsoft® Visual Basic® puede comunicarse con datos de Visual FoxPro mediante la creación de un control de datos que se conecta a un origen de datos de Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para conectarse a datos de Visual FoxPro mediante el Control de datos en Visual Basic  
  
1.  Cree un origen de datos denominado "test" que se conecte a la base de datos de ejemplo TasTrade incluida en Visual FoxPro. La instalación predeterminada de Visual FoxPro coloca la base de datos de ejemplo TasTrade en la ubicación:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  En Visual Basic, cree un nuevo formulario y coloque un cuadro de texto y un control De datos en él.  
  
3.  Cambie la propiedad Connect del control Data de la siguiente manera:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Cambie la propiedad RecordsetType a lo siguiente:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Cambie la propiedad RecordSource a lo siguiente:  
  
    ```  
    customer  
    ```  
  
6.  Cambie la propiedad DataSource del cuadro de texto por el nombre predeterminado del control Data por el siguiente:  
  
    ```  
    data1  
    ```  
  
7.  Cambie la propiedad DataField del cuadro de texto a lo siguiente:  
  
    ```  
    customer_id  
    ```  
  
8.  Ejecute el formulario y utilice el control Datos para omitir los campos de identificador de cliente de la base de datos de ejemplo de Visual FoxPro TasTrade.
