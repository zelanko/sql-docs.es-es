---
title: Agrupación de conexiones de administrador de controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efcd4c4b3dabc82b30d5b0e903dd8937ad3a7ce3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280419"
---
# <a name="driver-manager-connection-pooling"></a>Agrupación de conexiones de administrador de controladores
Agrupación de conexiones permite a una aplicación usar una conexión de un grupo de conexiones que no es necesario volver a establecerse para cada usuario. Una vez creada y colocada en un grupo de una conexión, una aplicación puede reutilizar esa conexión sin necesidad de realizar el proceso de conexión completa.  
  
 Uso de una conexión agrupada puede dar lugar a una mejora significativa del rendimiento, porque las aplicaciones pueden ahorrar la sobrecarga implicada en la creación de una conexión. Esto puede ser especialmente importante para las aplicaciones de nivel intermedio que se conectan a través de una red o para las aplicaciones que varias veces, conexión y desconexión, como las aplicaciones de Internet.  
  
 Además de mejoras de rendimiento, la arquitectura de agrupación de conexiones permite un entorno y sus conexiones asociadas para ser utilizada por varios componentes en un único proceso. Esto significa que pueden interactuar entre sí los componentes independientes en el mismo proceso sin conocer entre sí. Una conexión en un grupo de conexiones puede utilizarse varias veces por varios componentes.  
  
> [!NOTE]
>  Agrupación de conexiones puede utilizarse por una aplicación ODBC ODBC 2. *x* comportamiento, siempre y cuando la aplicación puede llamar a *SQLSetEnvAttr*. Cuando se usa la agrupación de conexiones, la aplicación no debe ejecutar instrucciones SQL que cambiar la base de datos o en el contexto de la base de datos, como cambiar la \< *base de datos ** nombre*>, que cambia el catálogo utilizado por un origen de datos.  


 Un controlador ODBC debe estar completamente segura para subprocesos y conexiones no deben tener afinidad de subprocesos para admitir la agrupación de conexiones. Esto significa que el controlador es capaz de controlar una llamada en cualquier subproceso en cualquier momento y puede conectarse en un subproceso, para usar la conexión en otro subproceso y desconectar en un tercer subproceso.  
  
 La agrupación de conexiones se mantiene mediante el Administrador de controladores. Las conexiones se extraen del grupo cuando la aplicación llama **SQLConnect** o **SQLDriverConnect** y se devuelven al grupo cuando la aplicación llama **SQLDisconnect**. El tamaño del grupo crece de forma dinámica, basándose en las asignaciones del recurso solicitado. Se reduce según el tiempo de espera de inactividad: Si una conexión está inactiva durante un período de tiempo (no se usó en una conexión), se quita del grupo. El tamaño del grupo está limitado únicamente por las restricciones de memoria y los límites en el servidor.  
  
 El Administrador de controladores determina si se debe usar una conexión específica en un grupo de acuerdo con los argumentos pasados **SQLConnect** o **SQLDriverConnect**y de acuerdo con los atributos de conexión establecer después de la conexión se ha asignado.  
  
 Cuando el Administrador de controladores es la agrupación de conexiones, debe ser capaz de determinar si una conexión todavía funciona antes de entregarlas de forma que la conexión. En caso contrario, el Administrador de controladores mantiene en repartir la conexión que no responde a la aplicación cada vez que se produce un error de red transitorios. Se ha definido un nuevo atributo de conexión de ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD. Este es un atributo de conexión de solo lectura que devuelve SQL_CD_TRUE o SQL_CD_FALSE. El valor SQL_CD_TRUE significa que la conexión ha perdido, mientras que el valor SQL_CD_FALSE significa que la conexión está activa. (Los controladores que se ajuste a las versiones anteriores de ODBC también pueden admitir este atributo.)  
  
 Un controlador debe implementar esta opción de forma eficaz o afectará el rendimiento de la agrupación de conexiones. En concreto, una llamada para obtener el atributo de conexión no debería causar un ida y vuelta al servidor. En su lugar, un controlador debe devolver solo el último estado conocido de la conexión. La conexión está inactivo si no se pudo la última ida y vuelta al servidor y no inactivo si se realizó correctamente en el último recorrido.  
  
## <a name="remarks"></a>Comentarios  
 Si una conexión se ha perdido (notifican a través de SQL_ATTR_CONNECTION_DEAD), el Administrador de controladores ODBC se destruirán esa conexión mediante una llamada a SQLDisconnect en el controlador. Nuevas solicitudes de conexión no pueden encontrar una conexión puede usar en el grupo. Finalmente, el Administrador de controladores puede crear una nueva conexión, suponiendo que el grupo está vacío.  
  
 Para usar un grupo de conexiones, una aplicación lleva a cabo los pasos siguientes:  
  
1.  Habilita la agrupación de conexiones mediante una llamada a **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Esta llamada debe realizarse antes de la aplicación asigna el entorno compartido para qué conexión de la agrupación es esté habilitado. El identificador del entorno en la llamada a **SQLSetEnvAttr** debe establecerse en null, lo que hace que SQL_ATTR_CONNECTION_POOLING un atributo de nivel de proceso. Si el atributo se establece en SQL_CP_ONE_PER_DRIVER, un grupo de conexiones solo se admite para cada controlador. Si una aplicación trabaja con muchos controladores y algunos entornos, esto sea más eficaz porque pueden requerir menos comparaciones. Si se admite el conjunto a SQL_CP_ONE_PER_HENV, un grupo de conexión único para cada entorno. Si una aplicación trabaja con muchos entornos y pocos controladores, esto sea más eficaz porque pueden requerir menos comparaciones. Agrupación de conexiones está deshabilitada estableciendo SQL_ATTR_CONNECTION_POOLING en SQL_CP_OFF.  
  
2.  Asigna un entorno mediante una llamada a **SQLAllocHandle** con el *HandleType* argumento establecido en SQL_HANDLE_ENV. El entorno asignado por esta llamada será un entorno compartido implícito porque se ha habilitado la agrupación de conexiones. No se ha determinado el entorno que se usará, no obstante, hasta **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama en este entorno.  
  
3.  Asigna una conexión mediante una llamada a **SQLAllocHandle** con *InputHandle* establecido en SQL_HANDLE_DBC y el *InputHandle* establecido en el identificador del entorno asignado para agrupación de conexiones. El Administrador de controladores intenta encontrar un entorno existente que coincide con los atributos de entorno establecidos por la aplicación. Si no existe ningún entorno de este tipo, se crea uno, con un recuento de referencias (mantenido por el Administrador de controladores) de 1. Si se encuentra un entorno compartido coincidente, el entorno se devuelve a la aplicación y su recuento de referencias se incrementa. (No viene determinada por el Administrador de controladores hasta que la conexión real que se usará **SQLConnect** o **SQLDriverConnect** se denomina.)  
  
4.  Las llamadas **SQLConnect** o **SQLDriverConnect** para realizar la conexión. El Administrador de controladores utiliza las opciones de conexión en la llamada a **SQLConnect** (o las palabras clave de conexión en la llamada a **SQLDriverConnect**) y establecen los atributos de conexión después de la asignación de la conexión a Determine qué conexión en el grupo debe usarse.  
  
    > [!NOTE]  
    >  Cómo se compara una conexión solicitada con una conexión agrupada viene determinada por el atributo de entorno SQL_ATTR_CP_MATCH. Para obtener más información, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Deben llamar las aplicaciones ODBC con la agrupación de conexiones [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante la inicialización de la aplicación y [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) cuando se cierra la aplicación.  
  
5.  Las llamadas **SQLDisconnect** cuando haya terminado con la conexión. La conexión se devuelve al grupo de conexiones y está disponible para su reutilización.  
  
 Para obtener información detallada, consulte [agrupación en el Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Consideraciones sobre la agrupación de conexiones  
 Llevar a cabo cualquier de las siguientes acciones mediante un comando SQL (en lugar de a través de la API de ODBC) puede afectar al estado de la conexión y provocar problemas inesperados cuando la agrupación de conexiones está activa:  
  
-   Abrir una conexión y cambiar la base de datos de forma predeterminada.  
  
-   Uso de la instrucción SET para cambiar alguna opción configurable (incluido SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, plan de presentación, estadísticas, TEXTSIZE y DATEFORMAT).  
  
-   Crear tablas temporales y procedimientos almacenados.  
  
 Si cualquiera de estas acciones se realizan fuera de la API de ODBC, la próxima persona que usa la conexión heredará automáticamente la configuración anterior, las tablas o procedimientos.  
  
> [!NOTE]  
>  No se espera que ciertas opciones de configuración estén presentes en el estado de conexión. Siempre debe establecer el estado de conexión en la aplicación y asegurarse de que la aplicación quita cualquier configuración de la agrupación de conexiones sin utilizar.  
  
## <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
 A partir de Windows 8, un controlador ODBC puede usar conexiones en el grupo de forma más eficaz. Para obtener más información, consulte [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a datos de un origen o el controlador](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación en Microsoft Data Access Components](https://go.microsoft.com/fwlink/?LinkId=120776)
