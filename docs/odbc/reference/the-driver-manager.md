---
title: El Administrador de controladores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c66acd08644176170c56700720a438aa8ffcdb1b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="the-driver-manager"></a>El Administrador de controladores
El *el Administrador de controladores* es una biblioteca que administra la comunicación entre las aplicaciones y controladores. Por ejemplo, en plataformas de Microsoft® Windows®, el Administrador de controladores es una biblioteca de vínculos dinámicos (DLL) que está escrita por Microsoft y puede distribuirse por los usuarios de MDAC 2.8 SP1 SDK redistribuible.  
  
 El Administrador de controladores existe principalmente por comodidad para los escritores de aplicaciones y soluciona muchos problemas comunes a todas las aplicaciones. Puede tratarse determinar qué controlador cargar basándose en un nombre de origen de datos, cargar y descargar controladores y llamar a funciones en los controladores.  
  
 Para ver por qué el segundo es un problema, tenga en cuenta lo que sucedería si la aplicación llama a funciones en el controlador directamente. A menos que la aplicación se vincula directamente a un controlador en particular, tendría una tabla de punteros a las funciones de ese controlador de compilación y llamar a esas funciones por puntero. Con el mismo código para más de un controlador a la vez agregar otro nivel de complejidad. La aplicación tendría en primer lugar establecer un puntero a función para que apunte a la función correcta en el controlador adecuado y, a continuación, llame a la función a través de ese puntero.  
  
 El Administrador de controladores se resuelve este problema, proporciona un único lugar para llamar a cada función. La aplicación se vincula a las funciones ODBC el Administrador de controladores y las llamadas en el Administrador de controladores, no el controlador. La aplicación identifica el origen de datos y el controlador de destino con un *identificador de conexión*. Cuando se carga un controlador, el Administrador de controladores compila una tabla de punteros a las funciones de ese controlador. Usa el identificador de conexión pasado la aplicación para encontrar la dirección de la función en el controlador de destino y llama a esa función por dirección.  
  
 En su mayor parte, el Administrador de controladores simplemente pasa las llamadas a funciones de la aplicación para el controlador adecuado. Sin embargo, también implementa algunas funciones (**SQLDataSources**, **SQLDrivers**, y **SQLGetFunctions**) y realiza comprobaciones de errores básicos. Por ejemplo, el Administrador de controladores comprueba que los identificadores no son punteros nulos, que se llaman a funciones en el orden correcto y que algunos argumentos de función no son válidos. Para obtener una descripción completa de los errores comprobados por el Administrador de controladores, consulte la sección de referencia para cada función y [tablas de transición de estado de apéndice B: ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 El rol principal final del Administrador de controladores se carga y descarga de controladores. La aplicación carga y descarga solo el Administrador de controladores. Cuando desea utilizar un controlador en particular, llama a una función de conexión (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**) en el Administrador de controladores y especifica el nombre de un origen de datos determinado o un controlador, por ejemplo, "Contabilidad" o "SQL Server". Con este nombre, el Administrador de controladores busca la información de origen de datos para el nombre de archivo del controlador, como Sqlsrvr.dll. A continuación, se carga el controlador (suponiendo que ya no está cargado), almacena la dirección de cada función en el controlador y llama a la función de conexión en el controlador, que, a continuación, inicializa y se conecta al origen de datos.  
  
 Cuando la aplicación ha terminado con el controlador, llama a **SQLDisconnect** en el Administrador de controladores. El Administrador de controladores llama a esta función en el controlador, que se desconecta del origen de datos. Sin embargo, el Administrador de controladores mantiene el controlador en la memoria en caso de que la aplicación vuelve a conectarse a él. Descarga el controlador solo cuando la aplicación libera la conexión usada por el controlador o usa la conexión para un controlador diferente, y ninguna otra conexión usa el controlador. Para obtener una descripción completa de rol del Administrador de controladores durante la carga y descarga de controladores, consulte [rol del Administrador de controladores en el proceso de conexión](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).

