---
title: El Administrador de controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c1ae3f098aea3886d5cb84a0bfcb7553a8181fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719731"
---
# <a name="the-driver-manager"></a>El Administrador de controladores
El *Administrador de controladores* es una biblioteca que administra la comunicación entre aplicaciones y controladores. Por ejemplo, en las plataformas de Microsoft® Windows®, el Administrador de controladores es una biblioteca de vínculos dinámicos (DLL) que está escrita por Microsoft y puede distribuirse por los usuarios de MDAC 2.8 SP1 SDK redistribuible.  
  
 El Administrador de controladores existe principalmente por comodidad para los escritores de aplicaciones y resuelve algunos problemas comunes a todas las aplicaciones. Estos incluyen determinar qué controlador cargar según un nombre de origen de datos, cargar y descargar controladores y llamar a funciones en los controladores.  
  
 Para ver por qué esto último es un problema, considere lo que sucedería si la aplicación llama a funciones en el controlador directamente. A menos que la aplicación se vincula directamente a un controlador en particular, tendría una tabla de punteros a las funciones de ese controlador de compilación y llamar a esas funciones por puntero. Con el mismo código para más de un controlador a la vez, agregaría otro nivel de complejidad. La aplicación podría primero tiene que establecer un puntero de función para que apunte a la función correcta en el controlador correcto y, a continuación, llame a la función a través de ese puntero.  
  
 El Administrador de controladores soluciona este problema proporcionando un único lugar para llamar a cada función. La aplicación se vincula a las funciones ODBC el Administrador de controladores y las llamadas en el Administrador de controladores, no el controlador. La aplicación identifica el origen de datos y el controlador de destino con un *identificador de conexión*. Cuando se carga un controlador, el Administrador de controladores crea una tabla de punteros a las funciones de ese controlador. Usa el identificador de conexión pasado la aplicación para buscar la dirección de la función en el controlador de destino y llama a esa función por dirección.  
  
 En su mayor parte, el Administrador de controladores simplemente pasa las llamadas de función de la aplicación para el controlador correcto. Sin embargo, también implementa algunas funciones (**SQLDataSources**, **SQLDrivers**, y **SQLGetFunctions**) y realiza la comprobación de errores básico. Por ejemplo, el Administrador de controladores comprueba que los identificadores no son punteros nulos, que se llama a funciones en el orden correcto y que ciertos argumentos de función son válidos. Para obtener una descripción completa de los errores comprobados por el Administrador de controladores, consulte la sección de referencia para cada función y [Apéndice B: Las tablas de transición de estado de ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 El rol principal final del Administrador de controladores se carga y descarga de controladores. La aplicación carga y descarga solo el Administrador de controladores. Cuando desea usar un controlador determinado, llama a una función de conexión (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**) en el Administrador de controladores y especifica el nombre de un origen de datos determinado o un controlador, por ejemplo, "Contabilidad" o "SQL Server". Con este nombre, el Administrador de controladores busca la información de origen de datos para el nombre de archivo del controlador, como Sqlsrvr.dll. A continuación, carga el controlador (suponiendo que ya no está cargado), almacena la dirección de cada función en el controlador y llama a la función de conexión en el controlador, que, a continuación, se inicializa y se conecta al origen de datos.  
  
 Cuando se realiza la aplicación con el controlador, llama **SQLDisconnect** en el Administrador de controladores. El Administrador de controladores, llama a esta función en el controlador, que se desconecta del origen de datos. Sin embargo, el Administrador de controladores mantiene el controlador en la memoria en caso de que la aplicación vuelve a conectarse a él. Descarga el controlador solo cuando la aplicación libera la conexión utilizada por el controlador o la conexión utiliza un controlador diferente y ninguna otra conexión usa el controlador. Para obtener una descripción completa de rol del Administrador de controladores en la carga y descarga de controladores, consulte [rol del Administrador de controladores en el proceso de conexión](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
