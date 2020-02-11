---
title: Conectar con un origen de datos (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e9e62c8e03166ec2f76b1c6bcb5000a062bac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082040"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectarse a un origen de datos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Una aplicación ODBC puede pasar información de conexión de varias maneras. Por ejemplo, la aplicación puede hacer que el controlador siempre pida al usuario la información de conexión. O bien, la aplicación podría esperar una cadena de conexión que especifique la conexión a un origen de datos. La forma de conectarse a un origen de datos depende del método de conexión utilizado por la aplicación ODBC.  
  
 Un método común para conectarse a un origen de datos es a través del cuadro de diálogo origen de datos. Si su aplicación ODBC está configurada para usar un cuadro de diálogo, se muestra ese cuadro de diálogo y se le pide la información de conexión del origen de datos correspondiente.  
  
 También puede conectarse a un origen de datos mediante la [cadena de conexión](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para conectarse a un origen de datos mediante un cuadro de diálogo  
  
1.  Cuando aparezca el cuadro de diálogo origen de datos, seleccione un origen de datos de Oracle y, a continuación, haga clic en Aceptar. Aparece el cuadro de diálogo conectar.  
  
2.  Rellene la información adecuada para el cuadro de diálogo conectar y, a continuación, haga clic en Aceptar.  
  
 Una vez comprobada la información de conexión, la aplicación puede usar el controlador ODBC para Oracle para tener acceso a la información que contiene el origen de datos.
