---
title: Conexión directa a los conductores (Conectándose directamente a los conductores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299085"
---
# <a name="connecting-directly-to-drivers"></a>Conectar directamente a los controladores
Como se ha explicado en Elegir un origen de [datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), anteriormente en esta sección, algunas aplicaciones no desean usar un origen de datos en absoluto. En su lugar, quieren conectarse directamente a un controlador. **SQLDriverConnect** proporciona una manera para que la aplicación se conecte directamente a un controlador sin especificar un origen de datos. Conceptualmente, se crea un origen de datos temporal en tiempo de ejecución.  
  
 Para conectarse directamente a un controlador, la aplicación especifica la palabra clave **DRIVER** en la cadena de conexión en lugar de la palabra clave **DSN.** El valor de la palabra clave **DRIVER** es la descripción del controlador devuelto por **SQLDrivers**. Por ejemplo, supongamos que un controlador tiene la descripción Controlador de Paradox y requiere el nombre de un directorio que contiene los archivos de datos. Para conectarse a este controlador, la aplicación puede utilizar cualquiera de las siguientes cadenas de conexión:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Con la primera cadena, el controlador no necesitaría ninguna información adicional. Con la segunda cadena, el controlador tendría que solicitar el nombre del directorio que contiene los archivos de datos.
