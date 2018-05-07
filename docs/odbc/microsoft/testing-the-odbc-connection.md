---
title: Probar la conexión ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba90587f40b3c7ef21f0dd1b6169ad6b0ab1b119
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="testing-the-odbc-connection"></a>Probar la conexión de ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Cuando solucione problemas de acceso ODBC para Oracle 7.x y servidores de Oracle8 RDBMS, podrían ser necesario comprobar que el código subyacente SQL * Net y adaptadores de protocolo de Oracle se han instalado correctamente. Para ello, use la utilidad suministrado por Oracle Nettest.exe en el directorio Orawin\Bin.  
  
 Nettest es una utilidad simple que intenta iniciar sesión en el servidor seleccionado con solo el instalado SQL * Net software que forma parte del cliente de Oracle. La utilidad le pedirá un nombre de inicio de sesión, contraseña y TNS cadena de conexión. Si el cliente de Oracle está instalado correctamente, la utilidad simplemente mostrará "Ping correcto." Si el inicio de sesión no se realizó correctamente, debe consultar a un administrador de base de datos.
