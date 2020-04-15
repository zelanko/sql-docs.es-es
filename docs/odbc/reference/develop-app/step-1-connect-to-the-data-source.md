---
title: 'Paso 1: Conéctese a la fuente de datos ( Data Source) Microsoft Docs'
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
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301355"
---
# <a name="step-1-connect-to-the-data-source"></a>Paso 1: Conexión al origen de datos
El primer paso en cualquier aplicación es conectarse al origen de datos. Esta fase, incluidas las funciones que requiere, se muestra en la siguiente ilustración.  
  
 ![Conexión a un origen de datos en una aplicación ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 El primer paso para conectarse al origen de datos es cargar el Administrador de controladores y asignar el identificador de entorno con **SQLAllocHandle**. Para obtener más información, consulte [Asignación del controlador](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)de entorno .  
  
 A continuación, la aplicación registra la versión de ODBC a la que se ajusta mediante una llamada a **SQLSetEnvAttr** con el atributo de entorno SQL_ATTR_APP_ODBC_VER. Para obtener más información, consulte [Declarar la versión ODBC de la aplicación](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) y Compatibilidad con [versiones anteriores y cumplimiento](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas .  
  
 A continuación, la aplicación asigna un identificador de conexión con **SQLAllocHandle** y se conecta al origen de datos con **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**. Para obtener más información, consulte [Asignación](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) de un controlador de conexión y [establecimiento de una conexión](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 A continuación, la aplicación establece los atributos de conexión, como si se deben confirmar manualmente las transacciones. Para obtener más información, consulte [Atributos](../../../odbc/reference/develop-app/connection-attributes.md)de conexión .
