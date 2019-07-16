---
title: Usar orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951800"
---
# <a name="using-data-sources"></a>Usar orígenes de datos
Orígenes de datos se crean normalmente por el usuario final o un técnico con un programa llamado el *Administrador ODBC*. El Administrador de ODBC solicita al usuario usar el controlador y, a continuación, llama a ese controlador. El controlador muestra un cuadro de diálogo que solicita la información que necesita para conectarse al origen de datos. Después de que el usuario escribe la información, el controlador lo almacena en el sistema.  
  
 Más adelante, la aplicación llama el Administrador de controladores y le pasa el nombre de un origen de datos de la máquina o la ruta de acceso de un archivo que contiene un origen de datos de archivo. Cuando se pasa un nombre de origen de datos de equipo, el Administrador de controladores busca en el sistema para buscar el controlador utilizado por el origen de datos. A continuación, carga el controlador y le pasa el nombre del origen de datos. El controlador usa el nombre del origen de datos para encontrar la información que necesita para conectarse al origen de datos. Por último, se conecta al origen de datos, suelen preguntar al usuario para un Id. de usuario y una contraseña, que generalmente no se almacenan.  
  
 Cuando se pasa a un origen de datos de archivo, el Administrador de controladores se abre el archivo y carga el controlador especificado. Si el archivo también contiene una cadena de conexión, pasa al controlador. Con la información de la cadena de conexión, el controlador se conecta al origen de datos. Si se ha pasado ninguna cadena de conexión, el controlador generalmente pide al usuario la información necesaria.
