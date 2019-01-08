---
title: SQLSetEnvAttr | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b0d30ac70ff3b7974f7d0530b9fb50494ac424
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354334"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  La [Referencia del programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) define cómo deben interpretar los controladores ODBC las especificaciones del atributo **SQLSetEnvAttr** desde aplicaciones escritas para la API de ODBC 2.*x* u ODBC 3.*x* . El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client cumple esas reglas.  
  
 Uno de los atributos controlado por **SQLSetEnvAttr** es si se utilizará la agrupación de conexiones. Si se utiliza la agrupación de conexiones con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, el parámetro *DriverCompletion* debe estar establecido en SQL_DRIVER_NOPROMPT al conectar con [SQLDriverConnect](sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLSetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
