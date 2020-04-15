---
title: Desarrollo de la conciencia de la agrupación de conexiones en un controlador ODBC Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283435"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC
En este tema se describen los detalles del desarrollo de un controlador ODBC que contiene información sobre cómo el controlador debe proporcionar servicios de agrupación de conexiones.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Habilitación de la agrupación de conexiones compatibles con el conductor  
 Un controlador debe implementar las siguientes funciones de interfaz de proveedor de servicios ODBC (SPI):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Consulte Referencia de la interfaz de proveedor de servicios [ODBC (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) para obtener más información.  
  
 Un controlador también debe implementar las siguientes funciones existentes para que se pueda habilitar la agrupación compatible con el controlador:  
  
|Función|Funcionalidad añadida|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Admite el nuevo tipo de identificador: SQL_HANDLE_DBC_INFO_TOKEN (consulte la descripción a continuación).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Admite el nuevo atributo de conexión set-only: SQL_ATTR_DBC_INFO_TOKEN para restablecer la conexión (consulte la descripción siguiente).|  
  
> [!NOTE]  
>  Las funciones en desuso como **SQLError** y **SQLSetConnectOption** no se admiten para la agrupación de conexiones con reconocimiento de controladores.  
  
## <a name="the-pool-id"></a>El ID de piscina  
 El identificador de grupo es un identificador específico del controlador de longitud de puntero para representar un grupo determinado de conexiones que se pueden usar indistintamente. Dado un conjunto de información de conexión, un controlador debe ser capaz de deducir rápidamente el identificador de grupo correspondiente.  
  
 Por ejemplo, el identificador del grupo debe codificar el nombre del servidor y la información de credenciales. Sin embargo, el nombre de la base de datos no es necesario porque un controlador puede reutilizar una conexión y, a continuación, cambiar la base de datos en menos tiempo que realizar una nueva conexión.  
  
 Un controlador debe definir un conjunto de atributos de clave, que comprenderá el identificador del grupo. El valor de estos atributos de clave puede provenir de atributos de conexión, cadena de conexión y DSN. En caso de que haya algún conflicto en estos orígenes, la directiva de resolución existente específica del controlador debe utilizarse para la compatibilidad con versiones anteriores.  
  
 El Administrador de controladores usará un grupo diferente para diferentes ideos de grupo. Todas las conexiones del mismo grupo son reutilizables. El Administrador de controladores nunca reutilizará una conexión con un identificador de grupo diferente.  
  
 Por lo tanto, los controladores deben asignar un identificador de grupo único para cada grupo de conexiones con el mismo valor en sus atributos de clave definidos. Si un controlador usa el mismo identificador de grupo para dos conexiones con valores diferentes en sus atributos de clave, el Administrador de controladores seguirá sin tenerlos en el mismo grupo (el Administrador de controladores no sabe nada acerca de los atributos de clave específicos del controlador). Esto significa que el controlador tendrá que informar al Administrador de controladores de que una conexión con un conjunto diferente de atributos de clave no es reutilizable dentro de [la función SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Esto puede disminuir el rendimiento y esto no se recomienda.  
  
 El Administrador de controladores no reutilizará una conexión asignada desde otro entorno de controlador, incluso si toda la información de conexión coincide. El Administrador de controladores usará un grupo diferente para diferentes entornos, incluso cuando las conexiones tienen el mismo identificador de grupo. Por lo tanto, el identificador del grupo es local para su entorno de controlador.  
  
 La función para obtener el identificador de grupo del controlador es [SQLGetPoolID (función).](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
## <a name="the-connection-rating"></a>La clasificación de conexión  
 En comparación con el establecimiento de una nueva conexión, puede obtener un mejor rendimiento restableciendo alguna información de conexión (como DATABASE) en una conexión agrupada. Por lo tanto, es posible que no desee que el nombre de la base de datos esté en el conjunto de atributos de clave. De lo contrario, puede tener un grupo independiente para cada base de datos, que puede no ser bueno en aplicaciones de nivel intermedio, donde los clientes usan varias cadenas de conexión diferentes.  
  
 Siempre que reutilice una conexión que tenga alguna discordancia de atributos, debe restablecer los atributos no coincidentes en función de la nueva solicitud de aplicación, de modo que la conexión devuelta sea idéntica a la solicitud de aplicación (consulte la explicación del atributo SQL_ATTR_DBC_INFO_TOKEN en [sqlSetConnectAttr Function](https://go.microsoft.com/fwlink/?LinkId=59368)). Sin embargo, restablecer esos atributos puede disminuir el rendimiento. Por ejemplo, restablecer una base de datos requiere una llamada de red al servidor. Por lo tanto, reutilice una conexión que se ajuste perfectamente, si hay una disponible.  
  
 Una función de clasificación en el controlador puede evaluar una conexión existente con una nueva solicitud de conexión. Por ejemplo, la función de clasificación del controlador puede determinar:  
  
-   Si la conexión existente se adapta perfectamente a la solicitud.  
  
-   Si solo hay algunas discrepancias insignificantes, como el tiempo de espera de conexión, que no requieren comunicación con el servidor para restablecer.  
  
-   Si hay algunos atributos no coincidentes que requieren una comunicación con el servidor para restablecer, pero seguiría nteniendo un mejor rendimiento que el establecimiento de una nueva conexión.  
  
-   Si se produjo la no coincidencia de un atributo que consume mucho tiempo para restablecer (el desarrollador del controlador puede considerar la posibilidad de agregar este atributo en el conjunto de atributos de clave, que se usa para generar el identificador del grupo).  
  
 Una puntuación entre 0 y 100 es posible, donde 0 significa no reutilizar y 100 significa perfectamente emparejado. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) es la función para calificar una conexión.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Nuevo controlador ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Para admitir la agrupación de conexiones compatible con controladores, el controlador necesita información de conexión para calcular el identificador de grupo. El controlador también necesita información de conexión para comparar nuevas solicitudes de conexión con conexiones en el grupo.  Siempre que no se pueda reutilizar ninguna conexión en el grupo, el controlador tiene que establecer una nueva conexión, por lo que requiere información de conexión.  
  
 Dado que la información de conexión puede provenir de varios orígenes (cadena de conexión, atributos de conexión y DSN), es posible que el controlador deba analizar la cadena de conexión y resolver el conflicto entre estos orígenes en cada una de las llamadas de función anteriores.  
  
 Por lo tanto, se introduce un nuevo identificador ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Con SQL_HANDLE_DBC_INFO_TOKEN, un controlador no necesita analizar la cadena de conexión y resolver conflictos en la información de conexión más de una vez. Dado que se trata de una estructura de datos específica del controlador, el controlador puede almacenar datos como información de conexión o identificador de grupo.  
  
 Este identificador solo se utiliza como interfaz entre el Administrador de controladores y el controlador. Una aplicación no puede asignar este identificador directamente.  
  
 El identificador primario de este identificador es de tipo SQL_HANDLE_ENV, lo que significa que el controlador puede obtener la información del entorno del identificador HENV durante la resolución de información de conexión.  
  
 Cada vez que recibe una nueva solicitud de conexión, el Administrador de controladores asignará un identificador de tipo SQL_HANDLE_DBC_INFO_TOKEN para almacenar información de conexión, después de confirmar que el controlador admite el reconocimiento del grupo de conexiones. Cuando haya terminado de usar el identificador (pero antes de devolver algunos códigos de retorno distintos de SQL_STILL_EXECUTING de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect),](../../../odbc/reference/syntax/sqlconnect-function.md)el Administrador de controladores liberará el identificador. Por lo tanto, el identificador se crea después de la sqlAllocHandle llamada y se destruye después de la SQLFreeHandle llamada. El Administrador de controladores garantiza que el identificador se liberará antes de liberar su HENV asociado (cuando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) devuelve un error).  
  
 El controlador debe modificar las siguientes funciones para aceptar el nuevo tipo de identificador SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 El Administrador de controladores garantiza que varios subprocesos no usarán el mismo identificador de SQL_HANDLE_DBC_INFO_TOKEN simultáneamente. Por lo tanto, el modelo de sincronización de este identificador puede ser muy simple dentro del controlador. El Administrador de controladores no tomará un bloqueo de entorno antes de asignar y liberar SQL_HANDLE_DBC_INFO_TOKEN.  
  
 **SQLAllocHandle** y **SQLFreeHandle** del Administrador de controladores no aceptarán este nuevo tipo de identificador.  
  
 SQL_HANDLE_DBC_INFO_TOKEN pueden contener información confidencial, como credenciales. Por lo tanto, un controlador debe borrar de forma segura el búfer de memoria (mediante [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) que contiene la información confidencial antes de liberar este identificador con **SQLFreeHandle**. Cada vez que se cierra el identificador de entorno de una aplicación, se cerrarán todos los grupos de conexiones asociados.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo de clasificación de la agrupación de conexiones de Driver Manager  
 En esta sección se describe el algoritmo de clasificación para la agrupación de conexiones del Administrador de controladores. Los desarrolladores de controladores pueden implementar el mismo algoritmo para la compatibilidad con versiones anteriores. Este algoritmo puede no ser el mejor. Debe refinar este algoritmo basado en la implementación (de lo contrario, no hay ninguna razón para implementar esta característica).  
  
 El Administrador de controladores devolverá una clasificación integral de 0 a 100 para cada conexión desde el grupo. 0 significa que la conexión no se puede reutilizar y 100 indica una coincidencia perfecta. Supongamos que la solicitud de conexión se denomina hRequest y que la conexión existente del grupo se denomina hCandidate. Si alguna de las siguientes condiciones es false, la conexión agrupada hCandidate no se puede reutilizar para hRequest (el Administrador de controladores asignará una calificación de 0).  
  
-   hCandidate y hRequest proceden de la API UNICODE (como SQLDriverConnectW) o de la API ANSI (como SQLDriverConnectA). (Los controladores UNICODE pueden tener un comportamiento diferente dado ANSI API y UNICODE API (consulte el atributo de conexión SQL_ATTR_ANSI_APP).)  
  
-   hCandidate y hRequest se crean mediante la misma función; SQLDriverConnect o SQLConnect.  
  
-   La cadena de conexión utilizada para abrir hCandidate debe ser la misma que hRequest, cuando se utiliza SQLDriverConnect.  
  
-   El NombreServidor (o DSN), el nombre de usuario y la contraseña utilizados para abrir hCandidate deben ser los mismos que se usan para abrir hRequest cuando se usa SQLConnect.  
  
-   El identificador de seguridad (SID) del subproceso actual debe ser el mismo que el SID utilizado para abrir hCandidate.  
  
-   Para el controlador que es caro dar de alta y no dar de alta (consulte la explicación de SQL_DTC_TRANSITION_COST en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), reutilizar *hRequest* no debe requerir una inscripción o unalista adicional.  
  
 En la tabla siguiente se muestra la asignación de puntuación para diferentes escenarios.  
  
|Comparación de los atributos de conexión entre la conexión agrupada y la solicitud|Sin inscripción / no inscripción|Requerir alistamiento adicional / no inscripción|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catálogo (SQL_ATTR_CURRENT_CATALOG) es diferente|60|50|  
|Algunos atributos de conexión son diferentes, pero el catálogo es el mismo|90|70|  
|Todos los atributos de conexión se adaptan perfectamente|100|80|  
  
## <a name="sequence-diagram"></a>Diagrama de secuencia  
 Este diagrama de secuencia muestra el mecanismo de agrupación básico descrito en este tema. Solo muestra el uso de [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) pero el caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) es similar.  
  
 ![Diagrama de secuencia](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagrama de estado  
 Este diagrama de estado muestra el objeto de token de información de conexión, que se describe en este tema. El diagrama solo muestra [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) pero el caso [sqlConnect](../../../odbc/reference/syntax/sqlconnect-function.md) es similar. Dado que el Administrador de controladores puede necesitar controlar los errores en cualquier momento, el Administrador de controladores puede llamar a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) para cualquier estado.  
  
 ![Diagrama de estado](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Consulte también  
 [Agrupación de conexiones conscientes del conductor](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Referencia de la interfaz del proveedor de servicios (SPI) de ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
