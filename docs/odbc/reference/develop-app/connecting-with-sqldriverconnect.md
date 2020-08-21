---
title: Conectando con SQLDriverConnect | Microsoft Docs
description: SQLDriverConnect proporciona funcionalidad de conexión adicional a través de SQLConnect, incluidas las opciones para solicitar al usuario más información.
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746175"
---
# <a name="connecting-with-sqldriverconnect"></a>Conexión con SQLDriverConnect

**SQLDriverConnect** se utiliza para conectarse a un origen de datos mediante una cadena de conexión. Se usa **SQLDriverConnect** en lugar de **SQLConnect** en los siguientes escenarios:  
  
- Establezca una conexión mediante una cadena de conexión que contenga el nombre del origen de datos, uno o varios identificadores de usuario, una o más contraseñas y otra información requerida por el origen de datos.  
  
- Establecer una conexión mediante una cadena de conexión parcial o sin información adicional; en este caso, el administrador de controladores y el controlador pueden pedir al usuario la información de conexión.  
  
- Establecer una conexión a un origen de datos que no está definida en la información del sistema. Si la aplicación proporciona una cadena de conexión parcial, el controlador puede solicitar al usuario la información de conexión.  
  
- Establezca una conexión a un origen de datos mediante una cadena de conexión construida a partir de la información de un archivo. DSN.  
  
Una vez establecida una conexión, **SQLDriverConnect** devuelve la cadena de conexión completa. La aplicación puede usar esta cadena para las solicitudes de conexión posteriores.

Esta sección contiene los temas siguientes.  
  
- [Información de conexión específicos del controlador](driver-specific-connection-information.md)  
  
- [Preguntar al usuario información de conexión](prompting-the-user-for-connection-information.md)  
  
- [Conectar con orígenes de datos de archivo](connecting-using-file-data-sources.md)  
  
- [Conectar directamente a los controladores](connecting-directly-to-drivers.md)
