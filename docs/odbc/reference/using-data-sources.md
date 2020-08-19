---
description: Usar orígenes de datos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 162f1c2bf8d75757ac2c29d60f675ac07ba8b00d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428846"
---
# <a name="using-data-sources"></a>Usar orígenes de datos
Los orígenes de datos suelen ser creados por el usuario final o un técnico con un programa llamado *Administrador de ODBC*. El administrador de ODBC solicita al usuario que use el controlador y, a continuación, llama a ese controlador. El controlador muestra un cuadro de diálogo que solicita la información necesaria para conectarse al origen de datos. Una vez que el usuario escribe la información, el controlador la almacena en el sistema.  
  
 Posteriormente, la aplicación llama al administrador de controladores y le pasa el nombre de un origen de datos de la máquina o la ruta de acceso de un archivo que contiene un origen de datos de archivo. Cuando se pasa un nombre de origen de datos de equipo, el administrador de controladores busca el controlador usado por el origen de datos en el sistema. A continuación, carga el controlador y le pasa el nombre del origen de datos. El controlador utiliza el nombre del origen de datos para encontrar la información que necesita para conectarse al origen de datos. Por último, se conecta al origen de datos, que normalmente solicita al usuario un identificador de usuario y una contraseña, que generalmente no se almacenan.  
  
 Cuando se pasa un origen de datos de archivo, el administrador de controladores abre el archivo y carga el controlador especificado. Si el archivo también contiene una cadena de conexión, lo pasa al controlador. Con la información de la cadena de conexión, el controlador se conecta al origen de datos. Si no se ha pasado ninguna cadena de conexión, el controlador normalmente solicita al usuario la información necesaria.
