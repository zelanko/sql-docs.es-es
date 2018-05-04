---
title: Agrupación de conexiones de administrador de controladores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69736f00cc4d357da0f6da7d4fbf3886144d1553
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager-connection-pooling"></a>Agrupación de conexiones de administrador de controladores
Agrupación de conexiones permite a una aplicación que utilice una conexión de un grupo de conexiones que no es necesario volver a establecer para cada usuario. Una vez creada y coloca en un grupo de una conexión, una aplicación puede reutilizar la conexión sin realizar el proceso de conexión completo.  
  
 Usar una conexión agrupada puede producir importantes mejoras de rendimiento, porque las aplicaciones ahorrará la sobrecarga implicada en realizar una conexión. Esto puede ser especialmente importante para las aplicaciones de nivel intermedio que se conectan a través de una red o para aplicaciones que se conectan repetidamente y desconexión, como aplicaciones de Internet.  
  
 Además de mejoras de rendimiento, la arquitectura de agrupación de conexiones permite a un entorno y sus conexiones asociadas para usarse en varios componentes en un único proceso. Esto significa que los componentes independientes en el mismo proceso pueden interactúan entre sí sin estar relacionados entre sí. Una conexión en un grupo de conexiones puede utilizar repetidamente en varios componentes.  
  
> [!NOTE]  
>  Agrupación de conexiones puede utilizarse con una aplicación ODBC presenta ODBC 2. *x* comportamiento, siempre y cuando la aplicación puede llamar a *SQLSetEnvAttr*. Cuando se usa la agrupación de conexiones, la aplicación no debe ejecutar instrucciones SQL que cambiar la base de datos o en el contexto de la base de datos, como cambiar la \< *base de datos ** nombre*>, que cambia el catálogo utilizado por un origen de datos.  
  
 Un controlador ODBC debe ser completamente segura para subprocesos y las conexiones no deben tener afinidad de subprocesos para admitir la agrupación de conexiones. Esto significa que el controlador es capaz de controlar una llamada en cualquier subproceso en cualquier momento y puede conectarse en un subproceso, para usar la conexión en otro subproceso y desconectar en un subproceso terceros.  
  
 La agrupación de conexiones se mantiene mediante el Administrador de controladores. Las conexiones se extraen del grupo cuando la aplicación llama **SQLConnect** o **SQLDriverConnect** y se devuelve al grupo cuando la aplicación llama **SQLDisconnect**. El tamaño del grupo crece dinámicamente, basándose en las asignaciones del recurso solicitado. Reduce según el tiempo de espera de inactividad: si una conexión está inactiva durante un período de tiempo (no se ha usado en una conexión), se quita del grupo. El tamaño del grupo está limitado únicamente por las restricciones de memoria y los límites en el servidor.  
  
 El Administrador de controladores determina si se debe usar una conexión específica en un grupo de acuerdo con los argumentos pasados en **SQLConnect** o **SQLDriverConnect**y de acuerdo con los atributos de conexión establecer después de que se asignó la conexión.  
  
 Cuando el Administrador de controladores es la agrupación de conexiones, debe ser capaz de determinar si una conexión sigue funcionando antes de entregar espera de la conexión. En caso contrario, el Administrador de controladores mantiene en repartir la conexión que no responde a la aplicación cada vez que se produce un error de red transitorios. Se ha definido un nuevo atributo de conexión de ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD. Se trata de un atributo de conexión de solo lectura que devuelva SQL_CD_TRUE o SQL_CD_FALSE. El valor SQL_CD_TRUE significa que la conexión se ha perdido, mientras que el valor SQL_CD_FALSE significa que la conexión está activa. (Controladores conforme a las versiones anteriores de ODBC también pueden admitir este atributo.)  
  
 Un controlador debe implementar eficazmente esta opción o afectará el rendimiento de la agrupación de conexiones. En concreto, una llamada para obtener el atributo de conexión no debería causar ida y vuelta al servidor. En su lugar, un controlador debe devolver el último estado conocido de la conexión. La conexión está inactivo si no se pudo el último recorrido en el servidor y no inactivas si se realizó correctamente en el último recorrido.  
  
## <a name="remarks"></a>Comentarios  
 Si una conexión se ha perdido (notificados a través de SQL_ATTR_CONNECTION_DEAD), el Administrador de controladores ODBC se destruirán esa conexión mediante una llamada a SQLDisconnect del controlador. Nuevas solicitudes de conexión no pueden encontrar una conexión utilizable en el grupo. Finalmente el Administrador de controladores puede realizar una conexión nueva, suponiendo que el grupo está vacío.  
  
 Para usar un grupo de conexiones, una aplicación realiza los pasos siguientes:  
  
1.  Habilita la agrupación de conexiones mediante una llamada a **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Esta llamada se debe realizar antes de que la aplicación asigna el entorno compartido para qué conexión agrupación es esté habilitado. El identificador de entorno en la llamada a **SQLSetEnvAttr** debe establecerse en null, lo que hace SQL_ATTR_CONNECTION_POOLING un atributo de nivel de proceso. Si el atributo se establece en SQL_CP_ONE_PER_DRIVER, un grupo de conexiones solo se admite para cada controlador. Si una aplicación trabaja con muchos controladores y algunos entornos, esto podría ser más eficaz porque pueden requerir menos comparaciones. Si se admite el conjunto a SQL_CP_ONE_PER_HENV, un grupo de conexión único para cada entorno. Si una aplicación funciona con pocos controladores y muchos entornos, esto podría ser más eficaz porque pueden requerir menos comparaciones. Agrupación de conexiones está deshabilitada estableciendo SQL_ATTR_CONNECTION_POOLING en SQL_CP_OFF.  
  
2.  Asigna un entorno mediante una llamada a **SQLAllocHandle** con el *HandleType* establecido en SQL_HANDLE_ENV. El entorno asignado por esta llamada será un entorno compartido implícita porque se ha habilitado la agrupación de conexiones. No se ha determinado el entorno que se usará, no obstante, hasta **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama en este entorno.  
  
3.  Asigna una conexión mediante una llamada a **SQLAllocHandle** con *InputHandle* establecido en SQL_HANDLE_DBC y el *InputHandle* establecer en el identificador de entorno asignado para agrupación de conexiones. El Administrador de controladores intenta encontrar un entorno existente que coincida con los atributos de entorno establecidos por la aplicación. Si no existe ningún entorno de este tipo, se crea uno, con un recuento de referencias (mantenido por el Administrador de controladores) de 1. Si se encuentra un entorno compartido coincidente, el entorno se devuelve a la aplicación y su recuento de referencias se incrementa. (Que se utilice la conexión real no está determinada por el Administrador de controladores hasta **SQLConnect** o **SQLDriverConnect** se denomina.)  
  
4.  Llamadas **SQLConnect** o **SQLDriverConnect** para realizar la conexión. El Administrador de controladores usa las opciones de conexión en la llamada a **SQLConnect** (o las palabras clave de conexión en la llamada a **SQLDriverConnect**) y establecen los atributos de conexión después de la asignación de la conexión a determinar qué conexión en el grupo se debe usar.  
  
    > [!NOTE]  
    >  El atributo de entorno SQL_ATTR_CP_MATCH determina cómo se compara con una conexión solicitada a una conexión agrupada. Para obtener más información, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Deben llamar las aplicaciones ODBC mediante la agrupación de conexiones [CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307) durante la inicialización de la aplicación y [CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310) cuando se cierra la aplicación.  
  
5.  Llamadas **SQLDisconnect** cuando haya terminado con la conexión. La conexión se devuelve al grupo de conexiones y deja de estar disponible para su reutilización.  
  
 Para obtener una explicación más detallada, vea [agrupación en Microsoft Data Access Components](http://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Consideraciones sobre la agrupación de conexiones  
 Llevar a cabo cualquiera de las siguientes acciones con un comando SQL (en lugar de a través de la API de ODBC) puede afectar al estado de la conexión y provocar problemas inesperados cuando la agrupación de conexiones está activa:  
  
-   Abrir una conexión y cambiar la base de datos de forma predeterminada.  
  
-   Usar la instrucción SET para cambiar las opciones configurables (incluidos SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, plan de presentación, las estadísticas, TEXTSIZE y DATEFORMAT).  
  
-   Crear tablas temporales y procedimientos almacenados.  
  
 Si alguna de estas acciones se realizan fuera de la API de ODBC, la próxima persona que usa la conexión heredará automáticamente la configuración anterior, tablas o los procedimientos.  
  
> [!NOTE]  
>  No se espera que ciertas opciones de configuración que esté presente en el estado de conexión. Siempre debe establecer el estado de conexión en la aplicación y asegúrese de que la aplicación quita cualquier configuración de la agrupación de conexiones no utilizadas.  
  
## <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
 A partir de Windows 8, un controlador ODBC puede usar conexiones en el grupo de forma más eficaz. Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a datos de un origen o el controlador](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación en Microsoft Data Access Components](http://go.microsoft.com/fwlink/?LinkId=120776)
