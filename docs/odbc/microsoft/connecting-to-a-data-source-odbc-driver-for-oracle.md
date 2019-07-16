---
title: Conectarse a un origen de datos (controlador ODBC para Oracle) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082040"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectarse a un origen de datos (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Una aplicación ODBC puede pasar información de conexión en varios aspectos. Por ejemplo, la aplicación podría tener el controlador siempre solicitarán al usuario información de conexión. O puede esperar a la aplicación de una cadena de conexión que especifica la conexión de origen de datos. Cómo conectarse a un origen de datos depende de la aplicación ODBC usado el método de conexión.  
  
 Es una forma habitual para conectarse a un origen de datos a través del cuadro de diálogo origen de datos. Si la aplicación ODBC se ha configurado para usar un cuadro de diálogo, cuadro de diálogo se muestra y le pide la información de conexión del origen de datos adecuado.  
  
 También puede conectarse a un origen de datos mediante el [cadena de conexión](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para conectarse a un origen de datos mediante un cuadro de diálogo  
  
1.  Cuando aparezca el cuadro de diálogo origen de datos, seleccione un origen de datos de Oracle y, a continuación, haga clic en Aceptar. Aparece el cuadro de diálogo Conectar.  
  
2.  Rellene la información apropiada para el cuadro de diálogo Conectar y, a continuación, haga clic en Aceptar.  
  
 Después de la conexión se comprueba información, la aplicación puede utilizar el controlador ODBC para Oracle para obtener acceso a la información que contiene el origen de datos.
