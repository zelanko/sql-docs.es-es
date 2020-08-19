---
description: El Administrador de controladores
title: Administrador de controladores | Microsoft Docs
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
ms.openlocfilehash: 70508eba3f5fce81c6f6185f0ec6befbe0d33b26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428877"
---
# <a name="the-driver-manager"></a>El Administrador de controladores
El *Administrador de controladores* es una biblioteca que administra la comunicación entre aplicaciones y controladores. Por ejemplo, en las plataformas de Microsoft® Windows®, el administrador de controladores es una biblioteca de vínculos dinámicos (DLL) escrita por Microsoft y se puede redistribuir por los usuarios del SDK de MDAC 2,8 SP1 redistribuible.  
  
 El administrador de controladores existe principalmente por comodidad para los escritores de aplicaciones y resuelve una serie de problemas comunes a todas las aplicaciones. Esto incluye determinar qué controlador cargar en función de un nombre de origen de datos, cargar y descargar controladores y llamar a funciones en los controladores.  
  
 Para ver por qué se trata de un problema, tenga en cuenta lo que sucedería si la aplicación llamara a funciones en el controlador directamente. A menos que la aplicación se haya vinculado directamente a un controlador determinado, tendría que crear una tabla de punteros a las funciones de ese controlador y llamar a esas funciones por puntero. Usar el mismo código para más de un controlador a la vez agregaría otro nivel de complejidad. En primer lugar, la aplicación tendría que establecer un puntero de función para que apunte a la función correcta en el controlador correcto y, a continuación, llamar a la función a través de ese puntero.  
  
 El administrador de controladores resuelve este problema proporcionando un solo lugar para llamar a cada función. La aplicación está vinculada al administrador de controladores y llama a las funciones ODBC en el administrador de controladores, no en el controlador. La aplicación identifica el controlador de destino y el origen de datos con un *identificador de conexión*. Cuando carga un controlador, el administrador de controladores crea una tabla de punteros a las funciones de ese controlador. Usa el identificador de conexión que pasa la aplicación para encontrar la dirección de la función en el controlador de destino y llama a esa función por dirección.  
  
 En su mayor parte, el administrador de controladores simplemente pasa las llamadas de función de la aplicación al controlador correcto. Sin embargo, también implementa algunas funciones (**SQLDataSources**, **SQLDrivers**y **SQLGetFunctions**) y realiza una comprobación de errores básica. Por ejemplo, el administrador de controladores comprueba que los identificadores no son punteros nulos, que se llama a las funciones en el orden correcto y que determinados argumentos de función son válidos. Para obtener una descripción completa de los errores que comprueba el administrador de controladores, consulte la sección de referencia de cada función y el [Apéndice B: tablas de transición de estado de ODBC](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 El rol principal final del administrador de controladores es cargar y descargar controladores. La aplicación carga y descarga solo el administrador de controladores. Cuando desea usar un controlador determinado, llama a una función de conexión (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) en el administrador de controladores y especifica el nombre de un origen de datos o un controlador determinados, como "contabilidad" o "SQL Server". Con este nombre, el administrador de controladores busca en la información del origen de datos el nombre de archivo del controlador, como Sqlsrvr.dll. A continuación, carga el controlador (suponiendo que no esté ya cargado), almacena la dirección de cada función en el controlador y llama a la función de conexión en el controlador, que se inicializa a continuación y se conecta al origen de datos.  
  
 Cuando la aplicación se realiza mediante el controlador, llama a **SQLDisconnect** en el administrador de controladores. El administrador de controladores llama a esta función en el controlador, que se desconecta del origen de datos. Sin embargo, el administrador de controladores mantiene el controlador en memoria en caso de que la aplicación se vuelva a conectar a él. Descarga el controlador solo cuando la aplicación libera la conexión usada por el controlador o usa la conexión para un controlador diferente y ninguna otra conexión utiliza el controlador. Para obtener una descripción completa del rol del administrador de controladores en la carga y descarga de controladores, consulte la [función del administrador de controladores en el proceso de conexión](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
