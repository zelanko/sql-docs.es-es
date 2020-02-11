---
title: Desarrollar el reconocimiento del grupo de conexiones en un controlador ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02577370218a799faf86a7f8986859c415962f5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897734"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC
En este tema se describen los detalles del desarrollo de un controlador ODBC que contiene información acerca de cómo el controlador debe proporcionar los servicios de agrupación de conexiones.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Habilitar la agrupación de conexiones compatible con controladores  
 Un controlador debe implementar las siguientes funciones de la interfaz del proveedor de servicios ODBC (SPI):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Consulte [referencia de la interfaz del proveedor de servicios ODBC (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) para obtener más información.  
  
 Un controlador también debe implementar las siguientes funciones existentes para que se pueda habilitar la agrupación compatible con controladores:  
  
|Función|Funcionalidad agregada|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Compatibilidad con el nuevo tipo de identificador: SQL_HANDLE_DBC_INFO_TOKEN (vea la descripción siguiente).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Compatibilidad con el nuevo atributo de conexión de solo conjunto: SQL_ATTR_DBC_INFO_TOKEN para restablecer la conexión (consulte la descripción siguiente).|  
  
> [!NOTE]  
>  No se admiten funciones desusadas como **SQLError** y **SQLSetConnectOption** para la agrupación de conexiones que reconocen el controlador.  
  
## <a name="the-pool-id"></a>El ID. del grupo  
 El identificador de grupo es un identificador específico del controlador de longitud de puntero que representa un grupo determinado de conexiones que se pueden usar indistintamente. Dado un conjunto de información de conexión, un controlador debe ser capaz de deducir rápidamente el identificador de grupo correspondiente.  
  
 Por ejemplo, el identificador de grupo debe codificar el nombre del servidor y la información de credenciales. Sin embargo, el nombre de la base de datos no es necesario porque un controlador puede volver a usar una conexión y, a continuación, cambiar la base de datos en menos tiempo que realizar una nueva conexión.  
  
 Un controlador debe definir un conjunto de atributos clave, que incluirán el identificador del grupo. El valor de estos atributos de clave puede proviene de los atributos de conexión, la cadena de conexión y el DSN. En caso de que haya conflictos en estos orígenes, se debe usar la Directiva de resolución específica del controlador existente para la compatibilidad con versiones anteriores.  
  
 El administrador de controladores usará un grupo diferente para los distintos ID. de grupo. Todas las conexiones del mismo grupo se pueden volver a usar. El administrador de controladores nunca volverá a usar una conexión con un identificador de grupo diferente.  
  
 Por lo tanto, los controladores deben asignar un identificador de grupo único para cada grupo de conexiones con el mismo valor en sus atributos de clave definidos. Si un controlador utiliza el mismo identificador de grupo para dos conexiones con valores diferentes en sus atributos clave, el administrador de controladores las colocará en el mismo grupo (el administrador de controladores no sabrá nada sobre los atributos de clave específicos del controlador). Esto significa que el controlador deberá notificar al administrador de controladores que no se puede volver a usar una conexión con un conjunto diferente de atributos clave dentro de la [función SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Esto puede reducir el rendimiento y esto no se recomienda.  
  
 El administrador de controladores no volverá a usar una conexión asignada desde otro entorno de controladores aunque coincida con toda la información de conexión. El administrador de controladores usará un grupo diferente para el entorno diferente, incluso cuando las conexiones tengan el mismo identificador de grupo. Por lo tanto, el identificador de grupo es local para su entorno de controlador.  
  
 La función para obtener el identificador de grupo del controlador es la [función SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>La clasificación de conexión  
 En comparación con el establecimiento de una nueva conexión, puede obtener un mejor rendimiento restableciendo parte de la información de conexión (como la base de datos) en una conexión agrupada. Por lo tanto, es posible que no desee que el nombre de la base de datos esté en el conjunto de atributos clave. De lo contrario, puede tener un grupo independiente para cada base de datos, que puede no ser bueno en las aplicaciones de nivel medio, donde los clientes usan varias cadenas de conexión diferentes.  
  
 Siempre que se reutiliza una conexión que tiene algún atributo que no coincide, se deben restablecer los atributos no coincidentes en función de la nueva solicitud de aplicación, de modo que la conexión devuelta sea idéntica a la solicitud de la aplicación (vea la descripción del atributo SQL_ATTR_DBC_INFO_TOKEN en la [función SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). Sin embargo, el restablecimiento de estos atributos puede reducir el rendimiento. Por ejemplo, restablecer una base de datos requiere una llamada de red al servidor. Por lo tanto, vuelva a usar una conexión que tenga una coincidencia perfecta, si hay alguna disponible.  
  
 Una función de clasificación en el controlador puede evaluar una conexión existente con una nueva solicitud de conexión. Por ejemplo, la función de clasificación del controlador puede determinar:  
  
-   Si la conexión existente coincide exactamente con la solicitud.  
  
-   Si solo hay algunas discrepancias insignificantes, como el tiempo de espera de conexión, que no requieren que se restablezca la comunicación con el servidor.  
  
-   Si hay algunos atributos no coincidentes que requieren una comunicación con el servidor para restablecerse, pero aun así darían un mejor rendimiento que establecer una nueva conexión.  
  
-   Si se produce un error de coincidencia para un atributo que tarda mucho tiempo en restablecerse (el desarrollador del controlador puede considerar agregar este atributo al conjunto de atributos clave, que se usa para generar el identificador del grupo).  
  
 Una puntuación entre 0 y 100 es posible, donde 0 significa que no se reutiliza y 100 significa que se ha encontrado una coincidencia. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) es la función para clasificar una conexión.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Nuevo identificador ODBC: SQL_HANDLE_DBC_INFO_TOKEN  
 Para admitir la agrupación de conexiones compatible con el controlador, el controlador necesita información de conexión para calcular el identificador del grupo. El controlador también necesita información de conexión para comparar las nuevas solicitudes de conexión con las conexiones del grupo.  Siempre que no se puede volver a usar una conexión en el grupo, el controlador tiene que establecer una nueva conexión, lo que requiere la información de conexión.  
  
 Dado que la información de conexión puede proviene de varios orígenes (cadena de conexión, atributos de conexión y DSN), es posible que el controlador necesite analizar la cadena de conexión y resolver el conflicto entre estos orígenes en cada una de las llamadas de función anteriores.  
  
 Por lo tanto, se introduce un nuevo identificador ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Con SQL_HANDLE_DBC_INFO_TOKEN, un controlador no necesita analizar la cadena de conexión y resolver conflictos en la información de conexión más de una vez. Dado que se trata de una estructura de datos específica del controlador, el controlador puede almacenar datos como la información de conexión o el identificador del grupo.  
  
 Este identificador solo se usa como una interfaz entre el administrador de controladores y el controlador. Una aplicación no puede asignar este identificador directamente.  
  
 El identificador primario de este identificador es de tipo SQL_HANDLE_ENV, lo que significa que el controlador puede obtener la información del entorno del identificador de HENV durante la resolución de la información de conexión.  
  
 Siempre que recibe una nueva solicitud de conexión, el administrador de controladores asignará un identificador de tipo SQL_HANDLE_DBC_INFO_TOKEN para almacenar la información de conexión, después de confirmar que el controlador admite el reconocimiento del grupo de conexiones. Cuando termine de usar el identificador (pero antes de devolver algunos códigos de retorno distintos de SQL_STILL_EXECUTING de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), el administrador de controladores liberará el identificador. Por lo tanto, el identificador se crea después de la llamada SQLAllocHandle y se destruye después de la llamada a SQLFreeHandle. El administrador de controladores garantiza que el identificador se liberará antes de liberar sus HENV asociadas (cuando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) devuelva un error).  
  
 El controlador debe modificar las siguientes funciones para aceptar el nuevo tipo de identificador SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 El administrador de controladores garantiza que varios subprocesos no usarán el mismo identificador de SQL_HANDLE_DBC_INFO_TOKEN simultáneamente. Por lo tanto, el modelo de sincronización de este controlador puede ser muy sencillo dentro del controlador. El administrador de controladores no realizará un bloqueo de entorno antes de asignar y liberar SQL_HANDLE_DBC_INFO_TOKEN.  
  
 El **SQLAllocHandle** y **SQLFreeHandle** del administrador de controladores no aceptarán este nuevo tipo de identificador.  
  
 SQL_HANDLE_DBC_INFO_TOKEN puede contener información confidencial, como las credenciales. Por lo tanto, un controlador debe borrar de forma segura el búfer de memoria (mediante [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) que contiene la información confidencial antes de liberar este identificador con **SQLFreeHandle**. Cada vez que se cierre el identificador de entorno de una aplicación, se cerrarán todos los grupos de conexiones asociados.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo de clasificación del grupo de conexiones del administrador de controladores  
 En esta sección se describe el algoritmo de clasificación para la agrupación de conexiones del administrador de controladores. Los desarrolladores de controladores pueden implementar el mismo algoritmo para la compatibilidad con versiones anteriores. Es posible que este algoritmo no sea el mejor. Debe refinar este algoritmo en función de su implementación (de lo contrario, no hay ningún motivo para implementar esta característica).  
  
 El administrador de controladores devolverá una clasificación integral de 0 a 100 para cada conexión del grupo. 0 significa que no se puede volver a usar la conexión y 100 indica que se ha encontrado una coincidencia perfecta. Suponga que la solicitud de conexión se denomina hRequest y que la conexión existente del grupo se denomina hCandidate. Si alguna de las siguientes condiciones es falsa, el hCandidate de conexión agrupado no se puede reutilizar para hRequest (el administrador de controladores asignará una clasificación de 0).  
  
-   hCandidate y hRequest proceden de una API Unicode (como SQLDriverConnectW) o de la API ANSI (como SQLDriverConnectA). (Los controladores Unicode pueden dar comportamiento a diferentes API ANSI y API Unicode (consulte el atributo de conexión SQL_ATTR_ANSI_APP)).  
  
-   hCandidate y hRequest se crean mediante la misma función. SQLDriverConnect o SQLConnect.  
  
-   La cadena de conexión utilizada para abrir hCandidate debe ser la misma que hRequest, cuando se usa SQLDriverConnect.  
  
-   Los nombres de servidor (o DSN), el nombre de usuario y la contraseña que se usan para abrir hCandidate deben ser los mismos que se usan para abrir hRequest cuando se usa SQLConnect.  
  
-   El identificador de seguridad (SID) del subproceso actual debe ser el mismo que el SID usado para abrir hCandidate.  
  
-   En el caso de los controladores que son caros de dar de alta y dar de baja (consulte la explicación de SQL_DTC_TRANSITION_COST en [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), reutilizar *hRequest* no debe requerir una inscripción adicional o una baja.  
  
 En la tabla siguiente se muestra la asignación de puntuación para diferentes escenarios.  
  
|Comparación de los atributos de conexión entre la conexión agrupada y la solicitud|Sin inscripción/baja|Requerir inscripción/desinscripción adicional|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catalog (SQL_ATTR_CURRENT_CATALOG) es diferente|60|50|  
|Algunos atributos de conexión son diferentes, pero el catálogo es el mismo|90|70|  
|Todos los atributos de conexión coinciden exactamente|100|80|  
  
## <a name="sequence-diagram"></a>Diagrama de secuencia  
 Este diagrama de secuencia muestra el mecanismo de agrupación básico que se describe en este tema. Solo muestra el uso de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , pero el caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) es similar.  
  
 ![Diagrama de secuencia](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagrama de estado  
 Este diagrama de estado muestra el objeto de token de información de conexión, que se describe en este tema. El diagrama solo muestra [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , pero el caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) es similar. Dado que el administrador de controladores puede tener que controlar los errores en cualquier momento, el administrador de controladores puede llamar a [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) para cualquier estado.  
  
 ![Diagrama de estado](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Consulte también  
 [Agrupación de conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Referencia de la interfaz del proveedor de servicios (SPI) de ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
