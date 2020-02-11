---
title: Orígenes de datos de equipo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- machine data sources [ODBC]
- data sources [ODBC], machine
ms.assetid: 371bb5b5-1258-4657-acb5-d2b688b2ab4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe58e6e560ce4a538290b9f87e99bb4f22e12aab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062644"
---
# <a name="machine-data-sources"></a>Orígenes de datos de equipo
Los *orígenes de datos* de la máquina se almacenan en el sistema con un nombre definido por el usuario. Asociado al nombre del origen de datos se encuentra toda la información que el administrador de controladores y el controlador necesitan para conectarse al origen de datos. Para un origen de datos xBase, podría ser el nombre del controlador xBase, la ruta de acceso completa del directorio que contiene los archivos xBase y algunas opciones que indican al controlador cómo usar esos archivos, como modo de usuario único o solo lectura. Para un origen de datos de Oracle, este podría ser el nombre del controlador de Oracle, el servidor en el que reside el DBMS de Oracle, la cadena de conexión de SQL *\*net que identifica el controlador de SQL Net que se va a usar y el ID. del sistema de la base de datos en el servidor.
