---
title: Agrupación de conexiones con reconocimiento de conductores (Driver-Aware Connection Pooling) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287605"
---
# <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador
La agrupación de conexiones consciente del controlador es una nueva característica del Administrador de controladores en Windows 8. La agrupación de conexiones con reconocimiento de controladores permite a los escritores de controladores personalizar el comportamiento de agrupación de conexiones en su controlador ODBC.  
  
> [!NOTE]  
>  La agrupación de conexiones con reconocimiento de controladores no se admite con la biblioteca de cursores. Una aplicación recibirá un mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando la agrupación de conexiones con reconocimiento de controladores está habilitada.  
  
 La agrupación de conexiones que reconoce el controlador soluciona los siguientes problemas relacionados con la agrupación de conexiones del Administrador de controladores:  
  
 **Fragmentación de la piscina** El Administrador de controladores solo devolverá una conexión del grupo si es una coincidencia exacta con la cadena de conexión de una nueva solicitud de conexión.  Una razón para que el Administrador de controladores requiera una coincidencia exacta es que el Administrador de controladores no entiende cada palabra clave de cadena de conexión específica del controlador y su valor.  Sin embargo, algunos valores de palabra clave de cadena de conexión (como el nombre de la base de datos) pueden no requerir una coincidencia exacta, ya que el controlador puede cambiar la base de datos en menos del tiempo necesario para abrir una nueva conexión (la diferencia de tiempo exacta depende del origen de datos). Además, las diferencias en algunos atributos de conexión (como SQL_ATTR_CURRENT_CATALOG) pueden tardar más tiempo en cambiar que las diferencias en otros atributos (como SQL_ATTR_LOGIN_TIMEOUT). Esto también puede impedir que el Administrador de controladores use la conexión reutilizable de menor costo desde el grupo. Cuando un controlador tiene que crear muchas conexiones nuevas, el rendimiento de una aplicación puede disminuir y la escalabilidad del origen de datos puede disminuir. La fragmentación del grupo se puede reducir con la agrupación de conexiones que reconoce el controlador porque un controlador puede estimar mejor el costo de reutilizar una conexión en el grupo para una solicitud de conexión.  
  
 **No se tiene en cuenta la preferencia de solicitud** Algunos orígenes de datos pueden abrir de forma eficaz nuevas conexiones (en comparación con el restablecimiento de algunos atributos), por lo que una aplicación puede preferir abrir una nueva conexión en lugar de intentar reutilizar una conexión ligeramente no coincidente del grupo y restablecer algunos valores (aunque esto puede ser más lento durante la frase de inicialización del grupo de conexiones). Pero algunas aplicaciones pueden mantener la carga del servidor más pequeña y abrir menos conexiones, aunque puede haber un costo mayor para corregir las discrepancias para un comportamiento correcto. Sin agrupación de conexiones compatible con el controlador, no puede especificar este tipo de preferencia de forma eficaz, porque el Administrador de controladores no reconoce todos los atributos de conexión específicos del controlador. La agrupación de conexiones con reconocimiento de controladores permite a un controlador obtener la preferencia del usuario (con un atributo específico del controlador de SQLSetConnectAttr) para que pueda estimar mejor el costo de reutilizar una conexión del grupo en función de la preferencia de un usuario.  
  
 Para obtener más información acerca de la agrupación de conexiones con reconocimiento de controladores, vea Desarrollar el reconocimiento de grupos de [conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinación del soporte del conductor  
 La agrupación de conexiones compatible con controladores es una característica opcional que un controlador puede no admitir. Para determinar si un controlador lo admite, use el *SQL_DRIVER_AWARE_POOLING_SUPPORTED InfoType* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Cómo habilitar la agrupación de conexiones con el controlador  
 Una aplicación puede usar el reconocimiento de agrupación de conexiones de un controlador estableciendo el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Si un controlador no admite el reconocimiento del grupo de conexiones, se usará la agrupación de conexiones del Administrador de controladores (igual que si se hubiera especificado SQL_CP_ONE_PER_HENV, en lugar de SQL_CP_DRIVER_AWARE). Las aplicaciones ODBC 2.x y 3.x pueden habilitar esta característica.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
