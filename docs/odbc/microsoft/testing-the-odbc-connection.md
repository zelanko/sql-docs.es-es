---
title: Prueba de la conexión ODBC ( ODBC Connection) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303116"
---
# <a name="testing-the-odbc-connection"></a>Probar la conexión de ODBC
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Al solucionar problemas de acceso ODBC a los servidores Oracle 7.x y Oracle8 RDBMS, es posible que sea necesario comprobar que los adaptadores de protocolo SQL*Net y Oracle subyacentes están instalados correctamente. Para ello, utilice la utilidad Nettest.exe proporcionada por Oracle en el directorio Orawin-Bin.  
  
 Nettest es una sencilla utilidad que intenta iniciar sesión en el servidor seleccionado utilizando solo el software SQL*Net instalado que forma parte del cliente de Oracle. La utilidad le pedirá un nombre de inicio de sesión, una contraseña y una cadena de conexión TNS. Si el cliente de Oracle está instalado correctamente, la utilidad simplemente mostrará "Ping Successful." Si el inicio de sesión no se realizó correctamente, deberá consultar con un administrador de la base de datos.
