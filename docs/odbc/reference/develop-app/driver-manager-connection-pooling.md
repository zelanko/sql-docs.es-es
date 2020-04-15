---
title: Agrupación de conexiones del Administrador de controladores (Driver Manager Connection Pooling) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305826"
---
# <a name="driver-manager-connection-pooling"></a>Agrupación de conexiones de administrador de controladores
La agrupación de conexiones permite a una aplicación utilizar una conexión desde un grupo de conexiones que no es necesario restablecer para cada uso. Una vez que se ha creado una conexión y se ha colocado en un grupo, una aplicación puede reutilizar esa conexión sin realizar el proceso de conexión completo.  
  
 El uso de una conexión agrupada puede dar lugar a mejoras significativas en el rendimiento, ya que las aplicaciones pueden ahorrar la sobrecarga implicada en la realización de una conexión. Esto puede ser especialmente significativo para las aplicaciones de nivel intermedio que se conectan a través de una red o para las aplicaciones que se conectan y desconectan repetidamente, como las aplicaciones de Internet.  
  
 Además de las mejoras de rendimiento, la arquitectura de agrupación de conexiones permite que varios componentes utilicen un entorno y sus conexiones asociadas en un único proceso. Esto significa que los componentes independientes en el mismo proceso pueden interactuar entre sí sin ser conscientes unos de otros. Una conexión en un grupo de conexiones se puede utilizar repetidamente por varios componentes.  
  
> [!NOTE]
>  La agrupación de conexiones puede ser utilizada por una aplicación ODBC que exhibe ODBC 2. *x* comportamiento, siempre que la aplicación pueda llamar a *SQLSetEnvAttr*. Cuando se usa la agrupación de conexiones, la aplicación no debe ejecutar instrucciones \<SQL que cambien la base de datos o el contexto de la base de datos, como cambiar el nombre de la *base* de datos>, lo que cambia el catálogo utilizado por un origen de datos.  


 Un controlador ODBC debe ser totalmente seguro para subprocesos y las conexiones no deben tener afinidad de subprocesos para admitir la agrupación de conexiones. Esto significa que el controlador puede controlar una llamada en cualquier subproceso en cualquier momento y puede conectarse en un subproceso, usar la conexión en otro subproceso y desconectarse en un tercer subproceso.  
  
 El Administrador de controladores mantiene el grupo de conexiones. Las conexiones se extraen del grupo cuando la aplicación llama a **SQLConnect** o **SQLDriverConnect** y se devuelven al grupo cuando la aplicación llama a **SQLDisconnect**. El tamaño del grupo crece dinámicamente, en función de las asignaciones de recursos solicitadas. Se reduce en función del tiempo de espera de inactividad: si una conexión está inactiva durante un período de tiempo (no se ha utilizado en una conexión), se quita del grupo. El tamaño del grupo está limitado únicamente por restricciones de memoria y límites en el servidor.  
  
 El Administrador de controladores determina si se debe usar una conexión específica en un grupo según los argumentos pasados en **SQLConnect** o **SQLDriverConnect**y según los atributos de conexión establecidos después de asignar la conexión.  
  
 Cuando el Administrador de controladores está agrupando conexiones, debe ser capaz de determinar si una conexión sigue funcionando antes de entregar la conexión. De lo contrario, el Administrador de controladores sigue repartiendo la conexión muerta a la aplicación cada vez que se produce un error de red transitorio. Se ha definido un nuevo atributo de conexión en ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD. Se trata de un atributo de conexión de solo lectura que devuelve SQL_CD_TRUE o SQL_CD_FALSE. El valor SQL_CD_TRUE significa que la conexión se ha perdido, mientras que el valor SQL_CD_FALSE significa que la conexión sigue activa. (Los controladores que se ajustan a versiones anteriores de ODBC también pueden admitir este atributo.)  
  
 Un controlador debe implementar esta opción de forma eficaz o perjudicará el rendimiento de la agrupación de conexiones. Específicamente, una llamada para obtener este atributo de conexión no debe causar un viaje de ida y vuelta al servidor. En su lugar, un controlador solo debe devolver el último estado conocido de la conexión. La conexión está agotada si el último viaje al servidor falla, y no está muerto si el último viaje se realizó correctamente.  
  
## <a name="remarks"></a>Observaciones  
 Si se ha perdido una conexión (notificada a través de SQL_ATTR_CONNECTION_DEAD), el Administrador de controladores ODBC destruirá esa conexión llamando a SQLDisconnect en el controlador. Es posible que las nuevas solicitudes de conexión no encuentren una conexión utilizable en el grupo. Eventualmente, el Administrador de controladores podría realizar una nueva conexión, suponiendo que el grupo está vacío.  
  
 Para utilizar un grupo de conexiones, una aplicación realiza los pasos siguientes:  
  
1.  Habilita la agrupación de conexiones mediante una llamada a **SQLSetEnvAttr** para establecer el atributo de entorno de SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Esta llamada debe realizarse antes de que la aplicación asigne el entorno compartido para el que se va a habilitar la agrupación de conexiones. El identificador de entorno en la llamada a **SQLSetEnvAttr** debe establecerse en null, lo que hace que SQL_ATTR_CONNECTION_POOLING un atributo de nivel de proceso. Si el atributo se establece en SQL_CP_ONE_PER_DRIVER, se admite un único grupo de conexiones para cada controlador. Si una aplicación funciona con muchos controladores y pocos entornos, esto podría ser más eficaz porque es posible que se requieran menos comparaciones. Si se establece en SQL_CP_ONE_PER_HENV, se admite un único grupo de conexiones para cada entorno. Si una aplicación funciona con muchos entornos y pocos controladores, esto podría ser más eficaz porque es posible que se requieran menos comparaciones. La agrupación de conexiones está deshabilitada estableciendo SQL_ATTR_CONNECTION_POOLING en SQL_CP_OFF.  
  
2.  Asigna un entorno llamando a **SQLAllocHandle** con el *HandleType* argumento establecido en SQL_HANDLE_ENV. El entorno asignado por esta llamada será un entorno compartido implícito porque se ha habilitado la agrupación de conexiones. Sin embargo, el entorno que se va a usar no se determina hasta que **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama en este entorno.  
  
3.  Asigna una conexión mediante una llamada a **SQLAllocHandle** con *InputHandle* establecido en SQL_HANDLE_DBC y el *InputHandle* establecido en el identificador de entorno asignado para la agrupación de conexiones. El Administrador de controladores intenta encontrar un entorno existente que coincida con los atributos de entorno establecidos por la aplicación. Si no existe tal entorno, se crea uno, con un recuento de referencias (mantenido por el Administrador de controladores) de 1. Si se encuentra un entorno compartido coincidente, el entorno se devuelve a la aplicación y se incrementa su recuento de referencias. (El Administrador de controladores no determina la conexión real que se va a utilizar hasta que se llama a **SQLConnect** o **SQLDriverConnect.)**  
  
4.  Llama a **SQLConnect** o **SQLDriverConnect** para realizar la conexión. El Administrador de controladores utiliza las opciones de conexión en la llamada a **SQLConnect** (o las palabras clave de conexión en la llamada a **SQLDriverConnect**) y los atributos de conexión establecidos después de la asignación de conexión para determinar qué conexión en el grupo se debe usar.  
  
    > [!NOTE]  
    >  El SQL_ATTR_CP_MATCH atributo de entorno determina cómo se coincide una conexión solicitada con una conexión agrupada. Para obtener más información, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Las aplicaciones ODBC que usan agrupación de conexiones deben llamar a [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante la inicialización de la aplicación y [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) cuando se cierra la aplicación.  
  
5.  Llama a **SQLDisconnect** cuando se hace con la conexión. La conexión se devuelve al grupo de conexiones y está disponible para su reutilización.  
  
 Para obtener una explicación detallada, consulte [Agrupación en los componentes](https://go.microsoft.com/fwlink/?LinkId=120776)de Microsoft Data Access .  
  
## <a name="connection-pooling-considerations"></a>Consideraciones de agrupación de conexiones  
 Realizar cualquiera de las siguientes acciones mediante un comando SQL (en lugar de a través de la API ODBC) puede afectar al estado de la conexión y causar problemas inesperados cuando la agrupación de conexiones está activa:  
  
-   Abrir una conexión y cambiar la base de datos predeterminada.  
  
-   Mediante la instrucción SET para cambiar las opciones configurables (incluidas SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, STATISTICS, TEXTSIZE y DATEFORMAT).  
  
-   Creación de tablas temporales y procedimientos almacenados.  
  
 Si alguna de estas acciones se realiza fuera de la API ODBC, la siguiente persona que usa la conexión heredará automáticamente la configuración, tablas o procedimientos anteriores.  
  
> [!NOTE]  
>  No espere que ciertas configuraciones estén presentes en el estado de conexión. Siempre debe establecer el estado de conexión en la aplicación y asegurarse de que la aplicación quita cualquier configuración de agrupación de conexiones no utilizada.  
  
## <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
 A partir de Windows 8, un controlador ODBC puede usar conexiones en el grupo de forma más eficaz. Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conexión a una fuente de datos o controlador](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupación en los componentes de Microsoft Data Access](https://go.microsoft.com/fwlink/?LinkId=120776)
