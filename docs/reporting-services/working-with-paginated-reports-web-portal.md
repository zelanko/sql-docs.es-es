---
title: Trabajar con informes paginados (portal web) | Documentos de Microsoft
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb0bc38f-dc56-4350-8457-cd135c0346e1
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: c6dcc44b05633004bd525d337c8303c1a8180121
ms.contentlocale: es-es
ms.lasthandoff: 07/03/2017

---

# Trabajar con informes paginados (portal web)
<a id="working-with-paginated-reports-web-portal" class="xliff"></a>

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Las propiedades de un informe paginado se pueden ver y administrar en el portal web. El portal web puede iniciar el Generador de informes para crear o editar informes paginados.  
   
## Crear un informe paginado
<a id="create-a-paginated-report" class="xliff"></a>  
  
Para crear un nuevo conjunto de datos compartido, puede hacer lo siguiente:  
  
1.  Seleccione Nuevo en la barra de menús.  
  
2.  Seleccione **Informe paginado**.  
  
    ![ssRSWebPortal-new-report](../reporting-services/media/ssrswebportal-new-report.png)  
  
3.  Se iniciará el Generador de informes o se le pedirá que lo descargue.  
  
4.  Cree el informe paginado y, después, seleccione el icono para **guardar** situado en la esquina superior izquierda para guardarlo en el servidor de informes.  
  
## Administrar un informe paginado existente
<a id="manage-an-existing-paginated-report" class="xliff"></a>  
  
Para administrar un informe paginado existente, puede hacer lo siguiente.  
  
> [!NOTE]
> Si no ve informes paginados en la carpeta, asegúrese de que está viendo informes paginados. Puede seleccionar **Ver** en la barra de menús de la esquina superior derecha del portal web. Procure que **Informes paginados** esté activado.  
  
1.  Seleccione el **puntos suspensivos (...)**  del conjunto de datos que desea administrar.  
      
    ![ssRSWebPortal-manage-report1](../reporting-services/media/ssrswebportal-manage-report1.png)  
  
2.  Seleccione **Administrar** , que le llevará a la pantalla de edición.  
    
    ![ssRSWebPortal-manage-report2](../reporting-services/media/ssrswebportal-manage-report2.png)  
  
## Propiedades
<a id="properties" class="xliff"></a>  
  
En la pantalla de propiedades, puede cambiar el **nombre** y la **descripción** del informe paginado. También puede usar las opciones **Eliminar**, **Mover**, **Crear informe vinculado**, **Editar en el Generador de informes**, **Descargar** o **Reemplazar**.  
    
![ssRSWebPortal-report-properties](../reporting-services/media/ssrswebportal-report-properties.png)  
   
## Parámetros
<a id="parameters" class="xliff"></a>  
  
Puede modificar los parámetros existentes de un informe paginado. Para agregar un nuevo parámetro, hay que editar el informe en el Generador de informes o en SQL Server Data Tools.  
  
![ssRSWebPortal-report-parameters](../reporting-services/media/ssrswebportal-report-parameters.png)  
   
## Origen de datos
<a id="data-source" class="xliff"></a>  
Puede apuntar a un origen de datos compartido o escribir la información de conexión correspondiente a un origen de datos personalizado.  
  
![ssRSWebPortal-report-datasource](../reporting-services/media/ssrswebportal-report-datasource.png)  
  
Para especificar un origen de datos personalizado, se usan las siguientes opciones.  
  
**Tipo**  
  
Especifique la extensión de procesamiento de datos que se va a usar para procesar los datos del origen de datos. Para obtener una lista de las extensiones de datos integradas, vea [Orígenes de datos admitidos por Reporting Services (SSRS)]. Es posible que otros fabricantes ofrezcan extensiones de procesamiento de datos adicionales.  
  
**Cadena de conexión**  
  
Especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. El tipo de conexión determina la sintaxis que debería usar. Por ejemplo, una cadena de conexión para la extensión de procesamiento de datos XML es una dirección URL a un documento XML. En la mayoría de los casos, la cadena de conexión típica especifica el servidor de bases de datos y un archivo de datos. En el siguiente ejemplo, se muestra la cadena de conexión usada para conectarse a una base de datos de SQL Server denominada MyData:  
  
    data source=(a SQL Server instance);initial catalog=MyData  
  
La cadena de conexión puede configurarse como expresión para que pueda especificar el origen de datos en tiempo de ejecución. Las expresiones de origen de datos se definen en el informe en el Diseñador de informes. Las expresiones de origen de datos no se pueden definir, ver ni modificar en el portal web. Sin embargo, una expresión de origen de datos se puede reemplazar haciendo clic en **Reemplazar predeterminado** para escribir una cadena de conexión estática. Si quiere recuperar la expresión, haga clic en **Volver al valor predeterminado**. El servidor de informes almacena la cadena de conexión original por si necesita restaurarla. Para usar expresiones de origen de datos, debe usar la información de conexión a un origen de datos que se publicó originalmente en el informe. Los orígenes de datos compartidos no admiten el uso de expresiones en la cadena de conexión.  
  
**Credenciales**  
  
Puede especificar la opción que determina cómo se obtienen las credenciales.  
  
> [!IMPORTANT]
> Si las credenciales se suministran en la cadena de conexión, se omiten las opciones y los valores que se proporcionan en esta sección. Tenga en cuenta que, si especifica las credenciales en la cadena de conexión, todos los usuarios que abran esta página verán los valores como texto no cifrado.  
  
**Como el usuario que visualiza el informe**  
  
Use las credenciales de Windows del usuario actual para obtener acceso al origen de datos. Seleccione esta opción cuando las credenciales que se usan para obtener acceso a un origen de datos son las mismas que se usaron para iniciar sesión en el dominio de red. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si Kerberos no está habilitado, las credenciales de Windows no se podrán pasar a otro servicio o equipo remoto. Si se requieren más conexiones de equipos, obtendrá un error en lugar de los datos esperados.  
  
Un administrador del servidor de informes puede deshabilitar el uso de seguridad integrada de Windows para tener acceso a los orígenes de datos del informe. Si este valor está deshabilitado, la característica no está disponible.  
  
No use esta opción si piensa programar o suscribirse a este informe. El procesamiento de informes desatendido o programado requiere credenciales que se pueden obtener sin datos proporcionados por el usuario o el contexto de seguridad de un usuario actual. Solo las credenciales almacenadas proporcionan esta capacidad. Por este motivo, el servidor de informes evita que programe el procesamiento de informes o suscripciones si el informe está configurado para el tipo de credencial de seguridad integrada de Windows. Si elige esta opción para un informe al que ya está suscrito o que tiene operaciones programadas, se detendrán las suscripciones y las operaciones programadas.  
  
**Con estas credenciales**  
  
Almacene un nombre de usuario y una contraseña cifrados en la base de datos del servidor de informes. Seleccione esta opción para ejecutar un informe de manera desatendida; por ejemplo, informes iniciados por programaciones o eventos en lugar de una acción del usuario.   
  
También puede elegir el tipo de credenciales, como la autenticación de Windows (nombre de usuario y contraseña de Windows) o una credencial de base de datos concreta (nombre de usuario y contraseña de la base de datos), como la autenticación de SQL.  
  
Si la cuenta es una credencial de Windows, la cuenta que especifique debe tener permisos de inicio de sesión local en el equipo que hospeda el origen de datos usado por el informe.  
  
Seleccione **Iniciar sesión con estas credenciales, pero luego intentar suplantar al usuario que visualiza el informe** para permitir la delegación de credenciales, pero solo si un origen de datos admite la suplantación. En el caso de las bases de datos de SQL Server, esta opción establece la función _SETUSER. En el caso de Analysis Services, se usa EffectiveUserName.  
  
**Pidiendo las credenciales al usuario que visualiza el informe**  
  
Cada usuario debe escribir un nombre de usuario y una contraseña para acceder al origen de datos. Puede definir el texto del mensaje que solicita las credenciales del usuario. Por ejemplo, "Escriba un nombre de usuario y una contraseña para acceder al origen de datos".  
  
También puede elegir el tipo de credenciales, como la autenticación de Windows (nombre de usuario y contraseña de Windows) o una credencial de base de datos concreta (nombre de usuario y contraseña de la base de datos), como la autenticación de SQL.  
  
**Sin credenciales**  
  
Esto hace que no sea necesario proporcionar las credenciales del origen de datos. Si un origen de datos necesita un inicio de sesión de usuario, esta opción no tendrá ningún efecto. Elija esta opción solo si la conexión al origen de datos no requiere credenciales de usuario.  
  
Para usar esta opción, debe haber configurado previamente la cuenta de ejecución desatendida para el servidor de informes. La cuenta de ejecución desatendida se usa para conectarse a los orígenes de datos externos cuando otros orígenes de credenciales no están disponibles. Si especifica esta opción y la cuenta no está configurada, se producirá un error en la conexión al origen de datos del informe y no se producirá el procesamiento de informes. Para más información sobre esta cuenta, vea [Configurar la cuenta de ejecución desatendida (Administrador de configuración de SSRS)](../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## Suscripciones
<a id="subscriptions" class="xliff"></a>  
Una suscripción de Reporting Services es una configuración que entrega un informe a una hora concreta o a raíz de un evento. Lo hace en el formato de archivo que especifique. Por ejemplo, todos los miércoles, se guarda el informe VentasMensuales en formato de documento Microsoft Word en un recurso compartido de archivos. Las suscripciones se pueden utilizar para programar y automatizar la entrega de un informe con un conjunto concreto de valores de parámetros de informes. Para obtener más información, consulte [trabajar con suscripciones](working-with-subscriptions-web-portal.md).
  
![ssRSWebPortal-report-subscription1](../reporting-services/media/ssrswebportal-report-subscription1.png)
   
## Elementos dependientes
<a id="dependent-items" class="xliff"></a>  
Use la página Elementos dependientes para ver una lista de los elementos que hacen referencia a este informe. El icono de cada tipo de elemento indica en qué consiste. A continuación, puede seleccionar la **puntos suspensivos (...)**  en cada elemento para administrar los elementos más adelante.  
  
## Almacenamiento en memoria caché
<a id="caching" class="xliff"></a>  
Dispone de varias opciones para almacenar en memoria caché los datos de un informe paginado. Puede empezar con una selección simple.  
  
1.  **Ejecutar este informe siempre con los datos más recientes** emitirá consultas al origen de datos cada vez que el informe se ejecute. Esto da como resultado un informe a petición que contiene los datos más actualizados. Cada vez que se abra el informe, se creará una instancia de este con los resultados de una nueva consulta. Cuando se usa esta opción, si diez usuarios abren el informe a la vez, se enviarán diez consultas para procesar al origen de datos.  
  
2.  **Realiza copias en caché de este informe y las usa cuando están disponibles** colocará una copia temporal de los datos en una memoria caché para poder usarla posteriormente. El almacenamiento en memoria caché suele mejorar el rendimiento porque los datos se devuelven desde la memoria caché en lugar de ejecutarse de nuevo la consulta del conjunto de datos. Con esta opción, si diez usuarios abren el informe, solamente la primera solicitud generará una consulta del origen de datos. El informe se almacena posteriormente en caché y los nueve usuarios restantes ven el informe almacenado en caché.  
  
3.  **Ejecutar siempre este informe según las instantáneas generadas previamente** almacenará en la memoria caché el diseño y los datos del informe durante un período de tiempo determinado. Los informes pueden ejecutarse como una instantánea de informe si se desea evitar que el informe se ejecute de forma arbitraria (durante una copia de seguridad programada, por ejemplo). La instantánea se puede actualizar según una programación. [Más información]  
  
![ssRSWebPortal-report-caching1](../reporting-services/media/ssrswebportal-report-caching1.png)  
   
Si selecciona **Cache Copies of this report and use them when available** (Almacenar en caché copias del informe y usarlas cuando estén disponibles), dispondrá de más opciones.  
  
![ssRSWebPortal-report-caching2](../reporting-services/media/ssrswebportal-report-caching2.png)  

Para obtener más información, consulte [trabajar con instantáneas](working-with-snapshots-web-portal.md).
  
### Expiración de la caché
<a id="cache-expiration" class="xliff"></a>  
  
Puede controlar si quiere que la memoria caché expire para el informe paginado transcurrido un tiempo determinado, o bien si prefiere hacerlo según una programación. Puede usar una programación compartida.  
  
> [!NOTE]
> La memoria caché no se actualiza.  
  
### Planes de actualización de caché
<a id="cache-refresh-plans" class="xliff"></a>  
  
Puede usar planes de actualización de caché a fin de crear programaciones para cargar previamente la memoria caché con copias temporales de datos de un informe paginado. Un plan de actualización incluye una programación y la opción para especificar o invalidar los valores de los parámetros. No puede invalidar los valores de los parámetros que estén marcados como de solo lectura. Puede crear y utilizar más de un plan de actualización.  
   
Las asignaciones de roles predeterminadas que permiten agregar, eliminar y cambiar los informes paginados para los planes de actualización de caché son Administrador de contenido, Mis informes y Publicador.  
  
Después de aplicar la opción de caché anterior, puede definir el plan de actualización de caché. Para ello, seleccione el vínculo **Manage Refresh Plans** (Administrar planes de actualización) que aparecerá tras aplicar la configuración de la caché. Se le llevará a la página de planes de actualización de caché.   
  
Para crear un nuevo plan de actualización de caché, seleccione **Nuevo plan de actualización de caché**. Después, puede escribir un nombre para el plan y especificar una programación. Si el conjunto de datos tiene parámetros definidos, verá que se enumeran y podrá especificar valores, a menos que estén marcados como de solo lectura.  
  
Cuando haya terminado, puede seleccionar **Create Cache Refresh Plan**(Crear plan de actualización de caché).  
  
![ssRSWebPortal-report-caching3](../reporting-services/media/ssrswebportal-report-caching3.png)  
  
> [!NOTE]
> El Agente SQL Server debe estar ejecutándose para poder crear un plan de actualización de caché.  
  
A continuación, puede **editar** o **eliminar** los planes que se muestren. La opción **Nuevo a partir de existente** se habilita cuando solo está seleccionado un plan de actualización de caché. Esta opción creará un plan de actualización nuevo que se copia a partir del plan original. El plan de actualización de caché se abre rellenado de antemano con detalles del plan que se seleccionara. A continuación puede modificar las opciones del plan de actualización y guardar el plan con otra descripción.  
  
## Instantáneas del historial
<a id="history-snapshots" class="xliff"></a>  
  
Use la página Instantáneas del historial para ver las instantáneas de informe que se han generado y almacenado a lo largo del tiempo. Según las opciones que se hayan configurado, es posible que el historial de informes solamente contenga las instantáneas más recientes.  
  
El historial del informe siempre se ve en el contexto del informe desde el que se origina. No se puede ver el historial de todos los informes de un servidor de informes en un solo lugar.  
  
Para generar una instantánea, el informe debe poder ejecutarse en modo desatendido, es decir, hay que usar credenciales almacenadas; los informes parametrizados deben contener valores predeterminados para todos los parámetros. Las instantáneas se pueden generar manualmente o como una operación programada.   
  
Puede hacer clic en una instantánea del historial de un informe para verla. Las instantáneas que aparecen en un historial de informe solamente se distinguen por la fecha y la hora en que fueron creadas. No hay manera de distinguir visualmente si una instantánea se generó como respuesta a una operación programada o manual.  
  
## Seguridad
<a id="security" class="xliff"></a>  
Use la página Propiedades de seguridad para ver o modificar la configuración de seguridad que determina el acceso al informe. Esta página está disponible para los elementos para los que tenga permiso de protección.  
  
El acceso a los elementos se define a través de asignaciones de roles, que especifican las tareas que puede realizar un grupo o usuario. Una asignación de roles consta de un nombre de usuario o grupo y de una o varias definiciones de roles que especifican un conjunto de tareas.  
  
**Editar seguridad del elemento**  
  
Seleccione para cambiar la manera en la que se define la seguridad para el elemento actual.

## Pasos siguientes
<a id="next-steps" class="xliff"></a>

[Portal Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabajar con conjuntos de datos compartidos](../reporting-services/work-with-shared-datasets-web-portal.md)

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
