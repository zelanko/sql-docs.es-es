---
title: El Administrador de controladores (Administrador de controladores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286799"
---
# <a name="the-driver-manager"></a>El Administrador de controladores
El *Administrador de controladores* es una biblioteca que administra la comunicación entre aplicaciones y controladores. Por ejemplo, en Microsoft® Windows® plataformas, el Administrador de controladores es una biblioteca de vínculos dinámicos (DLL) escrita por Microsoft y que pueden redistribuir los usuarios del SDK redistribuible de MDAC 2.8 SP1.  
  
 El Administrador de controladores existe principalmente como una comodidad para los escritores de aplicaciones y resuelve una serie de problemas comunes a todas las aplicaciones. Estos incluyen determinar qué controlador cargar en función de un nombre de origen de datos, cargar y descargar controladores y llamar a funciones en controladores.  
  
 Para ver por qué este último es un problema, considere lo que sucedería si la aplicación llamara funciones en el controlador directamente. A menos que la aplicación se vinculó directamente a un controlador determinado, tendría que crear una tabla de punteros a las funciones de ese controlador y llamar a esas funciones mediante puntero. Usar el mismo código para más de un controlador a la vez agregaría otro nivel de complejidad. La aplicación primero tendría que establecer un puntero de función para que apunte a la función correcta en el controlador correcto y, a continuación, llamar a la función a través de ese puntero.  
  
 El Administrador de controladores resuelve este problema proporcionando un único lugar para llamar a cada función. La aplicación está vinculada al Administrador de controladores y llama a funciones ODBC en el Administrador de controladores, no el controlador. La aplicación identifica el controlador de destino y el origen de datos con un identificador de *conexión.* Cuando se carga un controlador, el Administrador de controladores crea una tabla de punteros a las funciones de ese controlador. Utiliza el identificador de conexión pasado por la aplicación para buscar la dirección de la función en el controlador de destino y llama a esa función por dirección.  
  
 En su mayor parte, el Administrador de controladores solo pasa las llamadas de función de la aplicación al controlador correcto. Sin embargo, también implementa algunas funciones (**SQLDataSources**, **SQLDrivers**y **SQLGetFunctions**) y realiza la comprobación de errores básicos. Por ejemplo, el Administrador de controladores comprueba que los identificadores no son punteros nulos, que las funciones se llaman en el orden correcto y que ciertos argumentos de función son válidos. Para obtener una descripción completa de los errores comprobados por el Administrador de controladores, consulte la sección de referencia para cada función y [Apéndice B: Tablas](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
 El papel principal final del Administrador de controladores es cargar y descargar controladores. La aplicación carga y descarga solo el Administrador de controladores. Cuando desea utilizar un controlador determinado, llama a una función de conexión (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) en el Administrador de controladores y especifica el nombre de un origen de datos o controlador determinado, como "Contabilidad" o "SQL Server." Con este nombre, el Administrador de controladores busca en la información del origen de datos el nombre de archivo del controlador, como Sqlsrvr.dll. A continuación, carga el controlador (suponiendo que aún no está cargado), almacena la dirección de cada función en el controlador y llama a la función de conexión en el controlador, que, a continuación, se inicializa y se conecta al origen de datos.  
  
 Cuando la aplicación se realiza mediante el controlador, llama a **SQLDisconnect** en el Administrador de controladores. El Administrador de controladores llama a esta función en el controlador, que se desconecta del origen de datos. Sin embargo, el Administrador de controladores mantiene el controlador en la memoria en caso de que la aplicación se vuelva a conectar a él. Descarga el controlador solo cuando la aplicación libera la conexión utilizada por el controlador o utiliza la conexión para un controlador diferente, y ninguna otra conexión utiliza el controlador. Para obtener una descripción completa del rol del Administrador de controladores en la carga y descarga de controladores, consulte Rol del Administrador de [controladores en el proceso](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)de conexión .
