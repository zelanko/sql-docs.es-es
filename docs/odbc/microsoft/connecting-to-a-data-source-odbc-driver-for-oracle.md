---
title: Conectarse a un origen de datos (controlador ODBC para Oracle) | Documentos de Microsoft
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
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff9f7ab2cb1510309a7822cad5f2943d1c131ece
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectarse a un origen de datos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Una aplicación ODBC puede pasar información de conexión en una de varias maneras. Por ejemplo, la aplicación podría tener el controlador siempre solicitarán al usuario información de conexión. O bien, puede esperar a la aplicación de una cadena de conexión que especifica la conexión de origen de datos. Depende de cómo se conecte a un origen de datos en el método de conexión utilizado por la aplicación de ODBC.  
  
 Una manera común de conectarse a un origen de datos es a través del cuadro de diálogo origen de datos. Si la aplicación ODBC está configurada para usar un cuadro de diálogo, ese cuadro de diálogo aparece y le pide la información de conexión del origen de datos adecuado.  
  
 También puede conectarse a un origen de datos mediante la [cadena de conexión](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para conectarse a un origen de datos mediante un cuadro de diálogo  
  
1.  Cuando aparezca el cuadro de diálogo origen de datos, seleccione un origen de datos de Oracle y, a continuación, haga clic en Aceptar. Aparecerá el cuadro de diálogo Conectar.  
  
2.  Rellene la información apropiada para el cuadro de diálogo Conectar y, a continuación, haga clic en Aceptar.  
  
 Después de la conexión es comprobar información de la aplicación puede utilizar el controlador ODBC para Oracle para tener acceso a la información que contiene el origen de datos.
