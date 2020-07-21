---
title: Agrupación de conexiones compatible con controladores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287605"
---
# <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador
La agrupación de conexiones compatible con controladores es una característica nueva del administrador de controladores en Windows 8. La agrupación de conexiones compatible con controladores permite a los escritores de controladores personalizar el comportamiento de la agrupación de conexiones en el controlador ODBC.  
  
> [!NOTE]  
>  No se admite la agrupación de conexiones compatible con controladores con la biblioteca de cursores. Una aplicación recibirá un mensaje de error si intenta habilitar la biblioteca de cursores mediante SQLSetConnectAttr, cuando esté habilitada la agrupación de conexiones con reconocimiento de controladores.  
  
 La agrupación de conexiones compatible con controladores soluciona los siguientes problemas relacionados con la agrupación de conexiones del administrador de controladores:  
  
 **Fragmentación del grupo** El administrador de controladores solo devolverá una conexión del grupo si es una coincidencia exacta con la cadena de conexión de una nueva solicitud de conexión.  Una razón por la que el administrador de controladores requiere una coincidencia exacta es que el administrador de controladores no entiende cada palabra clave de cadena de conexión específica del controlador y su valor.  Sin embargo, es posible que algunos valores de la palabra clave de cadena de conexión (como el nombre de la base de datos) no requieran una coincidencia exacta, ya que el controlador puede cambiar la base de datos en menos tiempo necesario para abrir una nueva conexión (la diferencia de tiempo exacta depende del origen de datos). Además, las diferencias en algunos atributos de conexión (como SQL_ATTR_CURRENT_CATALOG) pueden tardar más tiempo en cambiar que las diferencias en otros atributos (como SQL_ATTR_LOGIN_TIMEOUT). También puede impedir que el administrador de controladores use la conexión reutilizable de menor costo del grupo. Cuando un controlador tiene que crear muchas conexiones nuevas, el rendimiento de una aplicación puede reducirse y la escalabilidad del origen de datos puede disminuir. La fragmentación del grupo se puede reducir con la agrupación de conexiones compatible con el controlador porque un controlador puede calcular mejor el costo de reutilizar una conexión en el grupo para una solicitud de conexión.  
  
 **Sin consideración de las preferencias de la aplicación** Algunos orígenes de datos pueden abrir eficazmente nuevas conexiones (en comparación con el restablecimiento de algunos atributos), por lo que es posible que una aplicación prefiera abrir una nueva conexión en lugar de intentar volver a usar una conexión ligeramente no coincidente del grupo y restablecer algunos valores (aunque esto puede ser más lento durante la frase de inicialización del grupo de conexiones). Pero algunas aplicaciones pueden mantener el servidor más pequeño y abrir menos conexiones, aunque puede haber un costo mayor de corregir las discrepancias para un comportamiento correcto. Sin la agrupación de conexiones compatible con controladores, no se puede especificar este tipo de preferencia de forma eficaz, ya que el administrador de controladores no reconoce todos los atributos de conexión específicos del controlador. La agrupación de conexiones compatible con controladores permite a un controlador obtener la preferencia del usuario (con un atributo específico del controlador de SQLSetConnectAttr) para que pueda calcular mejor el costo de reutilizar una conexión del grupo en función de la preferencia de un usuario.  
  
 Para obtener más información acerca de la agrupación de conexiones compatible con controladores, vea [desarrollar el reconocimiento del grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinar la compatibilidad con los controladores  
 La agrupación de conexiones compatible con controladores es una característica opcional que es posible que un controlador no admita. Para determinar si un controlador lo admite, use el SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Cómo habilitar la agrupación de conexiones compatible con controladores  
 Una aplicación puede usar el reconocimiento de la agrupación de conexiones de un controlador estableciendo el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_DRIVER_AWARE con [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Si un controlador no admite el reconocimiento del grupo de conexiones, se usará la agrupación de conexiones del administrador de controladores (igual que si se hubiera especificado SQL_CP_ONE_PER_HENV, en lugar de SQL_CP_DRIVER_AWARE). Las aplicaciones ODBC 2. x y 3. x pueden habilitar esta característica.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
