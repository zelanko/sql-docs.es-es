---
title: "Probar la conexión ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6875fa4ac03511b57239deadac748da1c37a0114
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="testing-the-odbc-connection"></a>Probar la conexión de ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Cuando solucione problemas de acceso ODBC para Oracle 7.x y servidores de Oracle8 RDBMS, podrían ser necesario comprobar que el código subyacente SQL * Net y adaptadores de protocolo de Oracle se han instalado correctamente. Para ello, use la utilidad suministrado por Oracle Nettest.exe en el directorio Orawin\Bin.  
  
 Nettest es una utilidad simple que intenta iniciar sesión en el servidor seleccionado con solo el instalado SQL * Net software que forma parte del cliente de Oracle. La utilidad le pedirá un nombre de inicio de sesión, contraseña y TNS cadena de conexión. Si el cliente de Oracle está instalado correctamente, la utilidad simplemente mostrará "Ping correcto." Si el inicio de sesión no se realizó correctamente, debe consultar a un administrador de base de datos.

