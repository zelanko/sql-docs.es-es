---
title: Uso de fuentes de datos ? Microsoft Docs
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
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286556"
---
# <a name="using-data-sources"></a>Usar orígenes de datos
Los orígenes de datos suelen ser creados por el usuario final o un técnico con un programa llamado *Administrador ODBC.* El Administrador ODBC solicita al usuario que use el controlador y, a continuación, llama a ese controlador. El controlador muestra un cuadro de diálogo que solicita la información que necesita para conectarse al origen de datos. Después de que el usuario introduce la información, el controlador la almacena en el sistema.  
  
 Más adelante, la aplicación llama al Administrador de controladores y le pasa el nombre de un origen de datos de máquina o la ruta de acceso de un archivo que contiene un origen de datos de archivo. Cuando se pasa un nombre de origen de datos de la máquina, el Administrador de controladores busca en el sistema para buscar el controlador utilizado por el origen de datos. A continuación, carga el controlador y le pasa el nombre del origen de datos. El controlador utiliza el nombre del origen de datos para buscar la información que necesita para conectarse al origen de datos. Por último, se conecta al origen de datos, normalmente solicitando al usuario un ID de usuario y una contraseña, que generalmente no se almacenan.  
  
 Cuando se pasa un origen de datos de archivo, el Administrador de controladores abre el archivo y carga el controlador especificado. Si el archivo también contiene una cadena de conexión, pasa esto al controlador. Con la información de la cadena de conexión, el controlador se conecta al origen de datos. Si no se ha pasado ninguna cadena de conexión, el controlador suele solicitar al usuario la información necesaria.
