---
description: 'Paso 1: Conexión al origen de datos'
title: 'Paso 1: conectar con el origen de datos | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ac15eed6c84745dca6406ad8186f14c65798939
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482968"
---
# <a name="step-1-connect-to-the-data-source"></a>Paso 1: Conexión al origen de datos
El primer paso de cualquier aplicación es conectar con el origen de datos. Esta fase, incluidas las funciones que requiere, se muestra en la siguiente ilustración.  
  
 ![Conexión a un origen de datos en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 El primer paso para conectar con el origen de datos es cargar el administrador de controladores y asignar el identificador de entorno con **SQLAllocHandle**. Para obtener más información, consulte [asignar el identificador de entorno](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 A continuación, la aplicación registra la versión de ODBC a la que se ajusta llamando a **SQLSetEnvAttr** con el atributo de entorno SQL_ATTR_APP_ODBC_VER. Para obtener más información, vea [declarar la versión de ODBC de la aplicación](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) y [compatibilidad con versiones anteriores y cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 A continuación, la aplicación asigna un identificador de conexión con **SQLAllocHandle** y se conecta al origen de datos con **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**. Para obtener más información, consulte [asignar un identificador de conexión](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) y [establecer una conexión](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 A continuación, la aplicación establece cualquier atributo de conexión, por ejemplo, si se confirman manualmente las transacciones. Para obtener más información, vea [atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).
