---
title: "Usar orígenes de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9ef21a59be0b292912a6ca4b4fc75a67dc952fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="using-data-sources"></a>Usar orígenes de datos
Orígenes de datos se crean normalmente por el usuario final o un técnico con un programa llamado el *Administrador ODBC*. El Administrador de ODBC solicita al usuario usar el controlador y, a continuación, llama a ese controlador. El controlador muestra un cuadro de diálogo que solicita la información que necesita para conectarse al origen de datos. Cuando el usuario introduce la información, el controlador almacena en el sistema.  
  
 Más adelante, la aplicación llama al administrador de controladores y le pasa el nombre de un origen de datos de la máquina o la ruta de acceso de un archivo que contiene un origen de datos de archivo. Cuando se pasa un nombre de origen de datos de máquina, el Administrador de controladores busca en el sistema para buscar el controlador utilizado por el origen de datos. A continuación, se carga el controlador y le pasa el nombre de origen de datos. El controlador utiliza el nombre de origen de datos para encontrar la información que necesita para conectarse al origen de datos. Por último, se conecta al origen de datos, normalmente preguntar al usuario para un Id. de usuario y una contraseña, que generalmente no se almacenan.  
  
 Cuando se pasa un origen de datos de archivo, el Administrador de controladores se abre el archivo y se carga el controlador especificado. Si el archivo también contiene una cadena de conexión, pasa al controlador. Con la información de la cadena de conexión, el controlador se conecta al origen de datos. Si no se pasa ninguna cadena de conexión, el controlador generalmente pide al usuario la información necesaria.
