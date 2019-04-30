---
title: Página nueva suscripción controlada por datos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 814b4653-572a-48c7-847f-b310ba0f3046
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 625afedabdb376f913d3353e2bda343bba66e3e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265949"
---
# <a name="create-data-driven-subscription-page-report-manager"></a>Página Crear suscripción controlada por datos (Administrador de informes)
  Use las páginas Crear suscripción controlada por datos para generar o modificar una suscripción que consulte una base de datos de suscriptor cada vez que se ejecuta la suscripción. Las suscripciones controladas por datos usan los resultados de la consulta para determinar los destinatarios de la suscripción, la configuración de entrega y los valores de parámetro de informe. En tiempo de ejecución, el servidor de informes ejecuta una consulta para obtener los valores utilizados para la configuración de la suscripción. Puede usar las páginas Crear suscripción controlada por datos para definir la consulta y asignar los valores de consulta a la configuración de suscripción. Los valores y las opciones que se especifican para una suscripción controlada por datos se reparten entre varias páginas, de manera similar a un asistente. En total, hay siete páginas.  
  
 Para crear una suscripción controlada por datos, es necesario saber cómo escribir una consulta o un comando que obtenga los datos de la suscripción. También debe tener un almacén de datos que contenga los datos de suscriptor (por ejemplo, nombres de suscriptor y direcciones de correo electrónico) para usarlos para la suscripción.  
  
 Esta página está disponible para los usuarios con permisos avanzados. Si se usa la seguridad predeterminada, no se pueden utilizar suscripciones controladas por datos en los informes situados en la carpeta Mis informes.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-data-driven-subscription-page"></a>Para abrir la página Suscripción controlada por datos  
  
1.  Abra el Administrador de informes y busque el informe para el que desea crear una suscripción controlada por datos.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades **General** correspondiente al informe.  
  
4.  Seleccione la pestaña **Suscripciones** y, a continuación, en **Nueva suscripción controlada por datos**.  
  
    > [!NOTE]  
    >  Para que este botón esté habilitado, el origen de datos de informe debe usar credenciales almacenadas.  
  
## <a name="start-a-subscription-page-1"></a>Iniciar una suscripción (página 1)  
 **Descripción**  
 Proporcione una descripción para la suscripción. La descripción aparece en la lista de suscripciones de **Mis suscripciones** y en la pestaña **Suscripciones** del informe.  
  
 **Especifique cómo se notifica a los destinatarios**  
 Seleccione la extensión de entrega que se va a utilizar para distribuir el informe. Para cada suscripción solo se puede utilizar una extensión de entrega. Las siguientes opciones están disponibles:  
  
-   Seleccione **Recurso compartido del Servidor de informes** para entregar informes a un recurso compartido de archivos. El informe se entregará como un archivo estático, desconectado del servidor de informes. Para más información, consulte [File Share Delivery in Reporting Services](subscriptions/file-share-delivery-in-reporting-services.md).  
  
-   Seleccione **Recurso compartido del Servidor de informes** para entregar informes a una bandeja de entrada de correo electrónico. Para más información, consulte [E-Mail Delivery in Reporting Services](subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Seleccione **Proveedor de entrega NULL** para entregar informes a la base de datos del servidor de informes. Esta opción crea instantáneas de informe. Elija esta opción cuando desee cargar previamente en el servidor de informes instantáneas de informe con parámetros o específicas del usuario según una programación determinada. Para más información, vea [Informes almacenados en caché &#40;SSRS&#41;](report-server/caching-reports-ssrs.md).  
  
 **Especifique un origen de datos que contiene la información del destinatario**  
 Especifique cómo se define la conexión al origen de datos. Puede elegir un origen de datos compartido si tiene uno que contenga la información de conexión necesaria. También puede especificar la información de conexión directamente en esta suscripción.  
  
 El origen de datos proporciona datos del suscriptor. Estos datos pueden ser nombres de empleados, id. de empleados, direcciones de correo electrónico y preferencias de formatos de exportación (como HTML o PDF). Si va a utilizar la extensión de entrega de correo electrónico del servidor de informes, el origen de datos debe contener direcciones de correo electrónico.  
  
## <a name="specify-a-connection-page-2"></a>Especificar una conexión (página 2)  
 Si especificó un origen de datos compartido, use esta página para seleccionar el elemento de origen de datos compartido. Puede utilizar el control de árbol para navegar hasta el elemento y seleccionarlo. Si va a definir una conexión para esta suscripción, use esta página para especificar las siguientes opciones:  
  
 **Tipo de conexión**  
 Seleccione la extensión de procesamiento de datos que desea usar con el origen de datos.  
  
 **Cadena de conexión**  
 Escriba la cadena de conexión que desea usar para conectar con el origen de datos.  
  
 **Conectar utilizando**  
 Escriba las credenciales que se van a utilizar para la conexión al origen de datos. Las credenciales se almacenan como valores cifrados en la base de datos del servidor de informes.  
  
 Si el origen de datos usa autenticación de Windows, seleccione **Usar como credenciales de Windows** al especificar la conexión.  
  
 Si está usando un origen de datos que no autentica las conexiones de usuario (por ejemplo, si el origen de datos es un archivo XML), seleccione No se necesitan credenciales. Esta opción requiere que haya configurado la cuenta de ejecución desatendida anteriormente. Para obtener más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="specify-a-query-page-3"></a>Especificar una consulta (página 3)  
 Use esta página para escribir la consulta que recupera los datos del suscriptor. Para obtener los mejores resultados, ejecute primero la consulta en SQL Server Management Studio, antes de usarla en la suscripción controlada por datos. A continuación, puede examinar los resultados para comprobar que contiene la información requerida. Los puntos importantes para reconocer los resultados de la consulta son:  
  
-   Las columnas del conjunto de resultados determinan los valores que se pueden especificar para las opciones de entrega y los parámetros de informe. Por ejemplo, si está creando una suscripción controlada por datos para la entrega de correo electrónico, debería tener una columna de direcciones de correo electrónico.  
  
-   Las filas del conjunto de resultados determinan el número de entregas de informes que se generan. Si tiene 10.000 filas, el servidor de informes generará 10.000 notificaciones y entregas.  
  
 **Consulta**  
 Especifique una consulta SQL o un comando que recupere un conjunto de resultados que contenga una fila para cada destinatario de la suscripción. En las páginas siguientes se usa el conjunto de resultados para rellenar la configuración de la extensión controlada por datos.  
  
 **Timeout**  
 Especifique un valor de tiempo de espera para la consulta. Este valor debe ser lo suficientemente grande para que se complete el procesamiento de la consulta.  
  
 **Validar**  
 Haga clic en **Validar** para comprobar la consulta. Para poder continuar, la consulta debe generar resultados válidos. Si no hace clic en **Validar**, se validará la consulta cuando haga clic en **Siguiente**.  
  
## <a name="set-delivery-options-page-4"></a>Establecer las opciones de entrega (página 4)  
 En la cuarta página se especifican las opciones de extensión de entrega. Las opciones que aparecen en la página se obtienen de la extensión de entrega. El modo en que especifique dichas opciones puede variar considerablemente según cómo la extensión de entrega las presente. Si la extensión no tiene valores, no aparecen opciones en esta página.  
  
|Seleccione|Para|  
|-----------------|----------------|  
|**Especifique un valor estático**|Usar un valor constante para la configuración de entrega. Algunas extensiones de entrega proporcionan valores estáticos para elegir. Por ejemplo, la entrega mediante correo electrónico del servidor de informes proporciona valores para **Incluir informe**, **Formato de representación**, **Prioridad**e **Incluir vínculo**.|  
|**Obtener el valor de la base de datos**|Usar un valor del conjunto de resultados. Las columnas del conjunto de resultados se pueden usar para proporcionar datos de suscriptor y valores de parámetros de informe.|  
|**Ningún valor**|Omite la configuración de la suscripción.|  
  
#### <a name="set-delivery-options-for-file-share-delivery"></a>Establecer opciones de entrega para la entrega a recursos compartidos de archivos  
 A menudo se usa la extensión de entrega a recursos compartidos de archivos porque no requiere ninguna configuración anterior. Si está usando la extensión de entrega a recursos compartidos de archivos, en la tabla siguiente se describe las opciones que se pueden establecer:  
  
 **Nombre de archivo**  
 Especifica un nombre de archivo para el informe. La extensión de entrega a recursos compartidos de archivos entrega un informe como un archivo de aplicación estático a una carpeta compartida. En la mayoría de los casos, debería usar un valor de la base de datos para crear el nombre de archivo. Dependiendo de la manera en que establece el modo de escritura, el uso de un valor estático hará que cada nueva entrega sobrescriba la anterior.  
  
 **Ruta de acceso**  
 Especifique una carpeta compartida que sea accesible a través de una conexión de red. Para comprobar que la carpeta es accesible, haga clic en **ejecutar** en el menú Inicio y escriba la ruta de acceso de carpeta con este formato: \\ \\< nombreDeEquipo\>\\< nombreCarpetaCompartida\>.  
  
 **Formato de representación**  
 Especifique el formato de salida del archivo. El servidor de informes puede escribir el archivo con formatos de aplicación de las extensiones de representación que están instaladas en el servidor de informes.  
  
 **Modo de escritura**  
 Especifique si el servidor de informes debería reemplazar un archivo con una versión más reciente, incrementarla o quitar la entrega si se encuentra un archivo del mismo nombre.  
  
 **Extensión de archivo**  
 Especifique True para anexar una extensión de archivo que coincida con el formato de representación seleccionado.  
  
 **Nombre de usuario.**  
 Escriba la cuenta de usuario de dominio que tenga permiso para agregar archivos a la carpeta compartida con este formato: \<dominio >\\< nombre de usuario\>.  
  
 **Contraseña**  
 Especifique la contraseña de la cuenta.  
  
## <a name="set-parameters-page-5"></a>Establecer parámetros (página 5)  
 Si un informe incluye parámetros, debe especificar qué valores de parámetro se van a usar con el informe. Los valores de los parámetros se pueden obtener del origen de datos del suscriptor (por ejemplo, si tiene un informe regional de ventas parametrizado basado en un código de región, puede obtener información de la región para cada empleado si esa información está almacenada en la base de datos de empleados).  
  
|Seleccione|Para|  
|-----------------|----------------|  
|**Especifique un valor estático**|Usar un valor constante para el parámetro si desea utilizar el mismo parámetro para todos los suscriptores. Si el parámetro tiene varios valores, puede elegir un valor en la lista.|  
|**Usar el valor predeterminado**|Algunos informes contienen un valor predeterminado para todos los parámetros o algunos de ellos. Si el parámetro de informe tiene un valor predeterminado, active esta casilla para usarlo.|  
|**Obtener el valor de la base de datos**|Usar un valor del conjunto de resultados. Las columnas del conjunto de resultados se pueden seleccionar como origen de un valor de datos que se utilizará con cada instancia de la suscripción.|  
  
## <a name="specify-a-trigger-page-6"></a>Especificar un desencadenador (página 6)  
 Seleccione un evento que inicia el procesamiento de suscripciones.  
  
|Seleccione|Para|  
|-----------------|----------------|  
|**Cuando se actualizan los datos del informe en el servidor de informes**|Si el informe está configurado para ejecutarse como instantánea de ejecución de informes, puede especificar que se ejecute la suscripción cuando se actualice la instantánea.|  
|**Según una programación creada para esta suscripción**|Ejecutar la suscripción en una fecha y a una hora específicas.|  
|**Según una programación compartida**|Ejecutar la suscripción utilizando la información de programación obtenida a través de una programación compartida.|  
  
## <a name="schedule-a-subscription-page-7"></a>Programar una suscripción (página 7)  
 Si programa la suscripción, debe especificar la frecuencia con la que se entrega el informe. El primer conjunto de opciones especifica una categoría de frecuencia (horaria, diaria, semanal, etc.). El segundo conjunto de opciones que aparece se basa en la selección inicial.  
  
 **Hourly**  
 Defina una programación que se ejecute a intervalos de horas.  
  
 **Diaria**  
 Defina una programación que se ejecute los días seleccionados a una hora específica. Puede especificar los días de las maneras siguientes: Cada  *\<día >*, todos los días laborables y cada  *\<número >* día. Al elegir un método se anulan los demás, aunque los demás días aparezcan seleccionados.  
  
 **Semanal**  
 Defina una programación que se ejecute en intervalos semanales a una hora específica. El intervalo puede ser una semana completa (por ejemplo, cada dos semanas) o días de una semana.  
  
 **Mensual**  
 Defina una programación que se ejecute mensualmente. En un mes, se puede elegir un día basándose en un modelo (por ejemplo, el último domingo de cada mes) o fechas específicas del calendario (como 1 y 15 para indicar los días uno y quince de cada mes). Puede utilizar comas y guiones para especificar varios días e intervalos; por ejemplo, 1, 5, 7-12, 21.  
  
 **Una vez**  
 Defina una programación que se ejecute una sola vez. Use la sección **Fechas de inicio y fin** para especificar el día en el que se va a ejecutar la programación. Esta programación deja de tener validez en cuanto se procesa.  
  
 **Fechas de inicio y finalización**  
 Especifique una fecha de inicio que determine cuándo entra en vigor la programación y una fecha de finalización que determine cuándo expira. Cuando las programaciones dejan de tener validez, no se notifica. Después de la fecha de finalización, ya no vuelven a ejecutarse.  
  
## <a name="saving-the-subscription"></a>Guardar la suscripción  
 Cuando hay información suficiente para la suscripción, se habilita el botón **Finalizar** . Haga clic en **Finalizar** para completar la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
