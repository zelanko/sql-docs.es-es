---
title: "Agrupación de conexiones dependientes del controlador | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 390d9801346f904e77647c1784d810672b45b6cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador
Agrupación de conexiones dependientes del controlador es una nueva característica del Administrador de controladores en Windows 8. Agrupación de conexiones dependientes del controlador permite que los escritores de controladores personalizar el comportamiento de su controlador ODBC de agrupación de conexiones.  
  
> [!NOTE]  
>  No se admite la agrupación de conexiones dependientes del controlador con la biblioteca de cursores. Una aplicación recibirá el mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando se habilita la agrupación de conexiones dependientes del controlador.  
  
 Direcciones de la agrupación de conexiones dependientes del controlador los siguientes problemas relacionados con la agrupación de conexiones de administrador de controladores:  
  
 **Fragmentación del grupo** el Administrador de controladores solo devolverá una conexión del grupo si es una coincidencia exacta con la cadena de conexión de una nueva solicitud de conexión.  Una razón para el Administrador de controladores para requerir a una coincidencia exacta es que el Administrador de controladores no entiende cada palabra clave de cadena de conexión específicos del controlador y su valor.  Sin embargo, algunos valores de palabra clave de cadena de conexión (por ejemplo, el nombre de la base de datos) no necesita a una coincidencia exacta, puesto que el controlador puede cambiar la base de datos en menos tiempo que el tiempo necesario para abrir una nueva conexión (la diferencia horaria exacta depende del origen de datos). Y las diferencias en algunos atributos de conexión (por ejemplo, SQL_ATTR_CURRENT_CATALOG) pueden tardar más tiempo para cambiar a las diferencias en otros atributos (por ejemplo, SQL_ATTR_LOGIN_TIMEOUT). Esto, también, puede evitar que el Administrador de controladores con la conexión de menor costo y reutilizable del grupo. Cuando un controlador tiene que crear muchas nuevas conexiones, puede reducir el rendimiento de la aplicación y puede reducir la escalabilidad del origen de datos. Fragmentación de grupos puede reducirse con la agrupación de conexiones dependientes del controlador porque un controlador mejor puede calcular el costo de volver a usar una conexión en el grupo para una solicitud de conexión.  
  
 **Sin tener en cuenta de preferencias de aplicación** algunos orígenes de datos eficazmente pueden abrir nuevas conexiones (comparado con el restablecimiento de algunos atributos), por lo tanto, quizás prefiera una aplicación abrir una nueva conexión en lugar de intentar volver a usar un ligeramente no coincidentes conexión del grupo y restablecimiento de algunos de los valores (aunque esto puede ser más lento durante la frase de inicialización de grupo de conexión). Pero algunas aplicaciones pueden reducir la carga del servidor y abra menos conexiones, aunque puede haber un costo mayor para corregir los errores de coincidencia para un comportamiento correcto. Sin agrupación de conexiones dependientes del controlador, no se puede especificar este tipo de preferencia de forma eficaz, porque el Administrador de controladores no reconoce todos los atributos de conexión específicos del controlador. Agrupación de conexiones dependientes del controlador permite que el controlador Obtenga la preferencia de usuario (con un atributo específico del controlador de SQLSetConnectAttr) para que mejor puede calcular el costo de volver a usar una conexión del grupo basado en la preferencia del usuario.  
  
 Para obtener más información acerca de la agrupación de conexiones dependientes del controlador, consulte [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinar la compatibilidad de controladores  
 Agrupación de conexiones dependientes del controlador es una característica opcional que un controlador no puede admitir. Para determinar si un controlador lo admite, use la SQL_DRIVER_AWARE_POOLING_SUPPORTED *tipo de información* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Cómo habilitar la agrupación de conexiones dependientes del controlador  
 Una aplicación puede usar el reconocimiento de agrupación de conexiones de un controlador estableciendo el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Si un controlador no es compatible con el conocimiento de la agrupación de conexiones, la agrupación de conexiones de administrador de controladores se usará (igual que si hubiera especificado SQL_CP_ONE_PER_HENV, en lugar de SQL_CP_DRIVER_AWARE). Las aplicaciones ODBC 2.x y 3.x pueden habilitar esta característica.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
