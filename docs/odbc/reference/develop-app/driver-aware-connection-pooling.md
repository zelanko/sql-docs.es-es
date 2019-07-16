---
title: Agrupación de conexiones dependientes del controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dee7ee2b08e4b3b0249ede7f999cfb23d8db944
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047052"
---
# <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador
Agrupación de conexiones dependientes del controlador es una nueva característica del Administrador de controladores en Windows 8. Agrupación de conexiones dependientes del controlador permite que los escritores de controladores personalizar el comportamiento en su controlador ODBC de agrupación de conexiones.  
  
> [!NOTE]  
>  No se admite la agrupación de conexiones dependientes del controlador con la biblioteca de cursores. Una aplicación recibirá el mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando está habilitada la agrupación de conexiones dependientes del controlador.  
  
 Direcciones de la agrupación de conexiones dependientes del controlador los siguientes problemas relacionados con la agrupación de conexiones de administrador de controladores:  
  
 **Fragmentación del grupo** el Administrador de controladores solo devolverá una conexión desde el grupo si es una coincidencia exacta con la cadena de conexión de una nueva solicitud de conexión.  Una razón para requerir a una coincidencia exacta para el Administrador de controladores es que el Administrador de controladores no entiende cada palabra clave de cadena de conexión específicos del controlador y su valor.  Sin embargo, es posible que algunos valores de palabra clave de cadena de conexión (por ejemplo, el nombre de la base de datos) no requieren a una coincidencia exacta, puesto que el controlador puede cambiar la base de datos menor que el tiempo necesario para abrir una nueva conexión (la diferencia horaria exacta depende del origen de datos). Además, las diferencias en algunos atributos de conexión (por ejemplo, SQL_ATTR_CURRENT_CATALOG) pueden tardar más tiempo para cambiar a las diferencias en otros atributos (por ejemplo, SQL_ATTR_LOGIN_TIMEOUT). Esto, también puede evitar que el Administrador de controladores mediante la conexión de menor costo y reutilizable del grupo. Cuando un controlador tiene que crear muchas nuevas conexiones, puede reducir el rendimiento de la aplicación y puede reducir la escalabilidad del origen de datos. Fragmentación de grupos puede reducirse con la agrupación de conexiones dependientes del controlador porque un controlador puede calcular mejor el costo de volver a usar una conexión en el grupo para una solicitud de conexión.  
  
 **Ninguna consideración de preferencia de la aplicación** algunos orígenes de datos eficaz pueden abrir nuevas conexiones (en comparación con el restablecimiento de algunos atributos), por lo tanto, quizás prefiera una aplicación abrir una nueva conexión en lugar de intentar volver a usar una que no coincide ligeramente conexión desde el grupo y el restablecimiento de algunos de los valores (aunque esto puede ser más lento durante la frase de inicialización del grupo de conexión). Pero algunas aplicaciones pueden mantener la carga del servidor más pequeños y abra admita menos conexiones, aunque puede haber un costo mayor para corregir las diferencias de comportamiento correcto. Sin agrupación de conexiones dependientes del controlador, no se puede especificar este tipo de preferencia de forma eficaz, porque el Administrador de controladores no reconoce todos los atributos de conexión específicos del controlador. Agrupación de conexiones dependientes del controlador permite que el controlador obtener la preferencia de usuario (con un atributo específico del controlador de SQLSetConnectAttr) para que puede calcular mejor el costo de volver a usar una conexión desde el grupo basado en la preferencia del usuario.  
  
 Para obtener más información sobre la agrupación de conexiones dependientes del controlador, vea [desarrollar el conocimiento de grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinar la compatibilidad de controladores  
 Agrupación de conexiones dependientes del controlador es una característica opcional que un controlador no puede admitir. Para determinar si un controlador lo admite, utilice el SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Cómo habilitar la agrupación de conexiones dependientes del controlador  
 Una aplicación puede usar el reconocimiento de agrupación de conexiones de un controlador estableciendo el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Si un controlador no es compatible con el conocimiento de la agrupación de conexiones, agrupación de conexiones de administrador de controladores se usará (igual que si hubieran sido especificados SQL_CP_ONE_PER_HENV, en lugar de SQL_CP_DRIVER_AWARE). Las aplicaciones ODBC 2.x y 3.x pueden habilitar esta característica.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
