---
title: Probar la conexión ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02509ddb6a986ebb7796d80aca10c6f18cde6e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939706"
---
# <a name="testing-the-odbc-connection"></a>Probar la conexión de ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Al solucionar el acceso ODBC a los servidores RDBMS de Oracle 7. x y Oracle8, puede que sea necesario comprobar que los adaptadores de protocolo SQL * Net y Oracle subyacentes están instalados correctamente. Para ello, use la utilidad proporcionada por Oracle. exe en el directorio Orawin\Bin  
  
 La red es una utilidad simple que intenta iniciar sesión en el servidor seleccionado usando únicamente el software SQL * Net instalado que forma parte del cliente de Oracle. La utilidad le pedirá un nombre de inicio de sesión, una contraseña y una cadena de conexión de TNS. Si el cliente de Oracle está instalado correctamente, la utilidad simplemente mostrará "ping successful". Si el inicio de sesión no se ha realizado correctamente, tendrá que consultar a un administrador de bases de datos.
