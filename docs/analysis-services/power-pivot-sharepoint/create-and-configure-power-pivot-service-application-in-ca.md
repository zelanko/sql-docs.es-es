---
title: "Crear y configurar la aplicación de servicio PowerPivot en la entidad emisora de certificados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 343e3ed597e892e7b9e332d35acb6719e5b27aee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-configure-power-pivot-service-application-in-ca"></a>Crear y configurar la aplicación de servicio PowerPivot en la entidad emisora de certificados
  Una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] es una instancia de servicio compartida del servicio de sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Cada aplicación de servicio tiene su propia identidad de aplicación, configuración, propiedades y almacenamiento de datos interno.  
  
 Este tema contiene las siguientes secciones:  
  
 [Determinación de si crear una nueva aplicación de servicio PowerPivot](#determine)  
  
 [Creación de una aplicación de servicio PowerPivot](#CreateApp)  
  
 [Configuración de la aplicación de servicio PowerPivot](#ConfigApp)  
  
 [Asignación de una aplicación de servicio PowerPivot a una aplicación web](#AssignGSA)  
  
 [Modificar las propiedades de la aplicación de servicio](#EditGSA)  
  
##  <a name="determine"></a> Determinación de si crear una nueva aplicación de servicio PowerPivot  
 Una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint debe tener al menos una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja. Las aplicaciones de servicio se crean automáticamente si utilizó la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configurar el servidor. Si no, debe crear una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] manualmente en Administración central.  
  
 Al crear una aplicación de servicio, el servicio estará disponible y se generará la base de datos de aplicación del servicio. En función de las opciones que seleccione al crear la aplicación de servicio, se agregará una conexión de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al grupo de conexiones de servicio predeterminado. Todas las aplicaciones web de SharePoint que se suscriban al grupo de conexiones de servicio predeterminado obtendrán automáticamente acceso inmediato a la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Puede crear varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Aunque con una aplicación de servicio basta en la mayoría de los escenarios de implementación, podría considerar la posibilidad de crear una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] más si entre los requisitos empresariales se hallan los siguientes:  
  
-   Usar una cuenta de actualización de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] desatendida diferente para cada aplicación.  
  
-   Usar distintos tiempos de espera, historial de uso y umbrales para los informes de respuesta de las consultas.  
  
-   Delegar la administración del servicio a distintas personas. Un administrador verá el historial de la actualización de datos, los datos de uso y otras propiedades solo para la aplicación que administra. Si tiene que aislar las aplicaciones web de SharePoint (por ejemplo, si su compañía es un servicio de hospedaje que necesita garantizar el aislamiento de los datos para las aplicaciones web de SharePoint que pertenecen a distintos clientes), crear aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] separadas puede ayudar a cumplir los requisitos de aislamiento, ya que garantiza que cada administrador de servicios vea solo la configuración y las propiedades de la aplicación que administra.  
  
 La creación de aplicaciones de servicio adicionales introduce nuevos requisitos para administrar las asociaciones del servicio. Sería necesario que creara y usara listas de asociaciones de servicios personalizadas para cada aplicación de servicio adicional que cree.  
  
 Si no tiene una razón concreta para crear una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] más, debería utilizar solo una para todas las aplicaciones web de la granja.  
  
##  <a name="CreateApp"></a> Creación de una aplicación de servicio PowerPivot  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta **Aplicaciones de servicio** , haga clic en **Nuevo**.  
  
3.  Seleccione **Aplicación de servicio de SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**. Si no aparece en la lista, significa que [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no se instaló o configuró correctamente.  
  
4.  En la página **Crear nueva aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, escriba un nombre para la aplicación. El valor predeterminado es PowerPivotServiceApplication\<número >. Si va a crear varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , un nombre descriptivo ayudará a otros administradores a saber cómo se utiliza la aplicación.  
  
5.  En Grupo de aplicaciones, cree un nuevo grupo de aplicaciones para la aplicación (recomendado). Seleccione o cree una cuenta administrada para el grupo de aplicaciones. No olvide especificar una cuenta de usuario de dominio. Una cuenta de usuario de dominio habilita el uso de la característica de cuentas administradas de SharePoint, que permite actualizar la información de cuentas y contraseñas en un solo lugar. Las cuentas de dominio también se necesitan si planea escalar la horizontalmente la implementación para incluir instancias de servicio adicionales que se ejecutarán bajo la misma identidad.  
  
6.  En **Servidor de bases de datos**, el valor predeterminado es la instancia del motor de base de datos de SQL Server que hospeda las bases de datos de configuración de la granja. Puede utilizar este servidor o elegir un servidor SQL Server diferente.  
  
7.  En **nombre de base de datos**, el valor predeterminado es PowerPivotServiceApplication1_\<guid >. Debe crear una base de datos única para cada aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . El nombre predeterminado de la base de datos corresponde al de la aplicación de servicio. Si escribió un nombre de aplicación del servicio único, siga una convención de nomenclatura similar para el nombre de la base de datos, de modo que pueda administrarlos juntos.  
  
8.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la guía del administrador de SharePoint para obtener información sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. De manera opcional, active la casilla **Agregue el proxy de esta aplicación de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al grupo de proxy predeterminado.** De esta forma se agrega la conexión de la aplicación de servicio al grupo de conexiones de servicio predeterminado.  
  
     Debe activar esta casilla si está creando la primera aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Debe haber una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el grupo de conexiones predeterminado para que el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] funcione correctamente.  
  
     No agregue la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al grupo de conexiones predeterminado si ya hay una. Agregar varias entradas del mismo tipo de aplicación de servicio no se admite y podría producir errores. Si está creando aplicaciones de servicio adicionales, déjelas fuera del grupo de conexiones predeterminado y agréguelas a listas personalizadas.  
  
     Para más información sobre las asociaciones del servicio, vea [Conectar una aplicación de servicio PowerPivot a una aplicación web de SharePoint en Administración central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Haga clic en **Aceptar.** La aplicación de servicio aparecerá junto a otros servicios administrados en la lista de aplicaciones de servicio de la granja.  
  
##  <a name="ConfigApp"></a> Configuración de la aplicación de servicio PowerPivot  
 Una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nueva se crea usando una configuración predeterminada. La configuración predeterminada se recomienda en la mayoría de los escenarios. Cámbiela únicamente si se percata de que el tiempo de respuesta es lento o que se quitan conexiones, o si va a variar la configuración de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para aplicaciones web de SharePoint concretas.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
     En la lista de aplicaciones de servicio, debería ver la aplicación de servicio que ha creado y denominado. El valor predeterminado es **PowerPivotServiceApplication1**.  
  
2.  Haga clic en el nombre de aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se abrirá el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  En la lista **Acciones** en la esquina superior derecha del panel, haga clic en **Configurar las opciones de aplicación de servicio**.  
  
4.  En **Tiempo de espera de carga de base de datos**, aumente o disminuya el valor para cambiar durante cuánto tiempo el servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] espera una respuesta de la instancia de SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) a la que se ha enviado una solicitud de datos de carga. Dado que los conjuntos de datos muy grandes tardan tiempo en atravesar la conexión, debe permitir el tiempo suficiente para que la instancia de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] recupere el libro de Excel y mueva los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una instancia de Analysis Services para que se procesen las consultas. Como los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pueden ser extraordinariamente grandes, el valor predeterminado es de 30 minutos.  
  
5.  En **Tiempo de espera del grupo de conexiones**, aumente o disminuya el valor para cambiar el número de minutos que una conexión de datos inactiva permanecerá abierta. El valor predeterminado es de 30 minutos. Durante este período, la aplicación del servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] reutilizará una conexión de datos inactiva para las solicitudes de solo lectura del mismo usuario de SharePoint para los mismos datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si no se reciben más solicitudes para esos datos durante el período especificado, la conexión se quita del conjunto. Los valores válidos van de 1 a 3600 segundos. Para más información sobre cómo conectar grupos, vea [Referencia de las opciones de configuración &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md).  
  
6.  En **Tamaño máximo de grupo de conexiones de usuario**, aumente o disminuya el valor para cambiar el número máximo de conexiones inactivas que el servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creará en grupos de conexiones individuales para cada usuario de SharePoint, conjunto de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y combinaciones de versión.  
  
     El valor predeterminado es de 1000 conexiones inactivas. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de usuario), o de 1 a 10000.  
  
     Estos grupos de conexiones permiten al servicio admitir más eficazmente conexiones continuadas a los mismos datos de solo lectura del mismo usuario. Si deshabilita la agrupación de conexiones, cada conexión se creará como nueva.  
  
     Observe que cambiar el límite del tamaño del grupo de conexiones, incluso si se establece en 0, no hará que se quiten conexiones. Los grupos de conexiones existen para reducir los tiempos de espera al conectar a los datos. El servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nunca denegará una conexión según la configuración del grupo de conexiones.  
  
7.  En **Tamaño máximo del grupo de conexiones de administración**, aumente o disminuya el valor para cambiar el número de conexiones abiertas en un grupo de conexiones creado para una conexión de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a Analysis Services. Cada instancia de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] abre una conexión administrativa independiente con la instancia de Analysis Services en el mismo equipo. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] crea un grupo independiente para reutilizar las conexiones administrativas con el propósito de comprobar si hay conexiones inactivas y supervisar el estado del servidor. El valor predeterminado es de 200 conexiones. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de administrador), o de 1 a 10.000. Si selecciona 0, cada conexión se creará como nueva.  
  
8.  En **Método de asignación**, puede especificar el esquema del equilibrio de carga que el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] utiliza para seleccionar una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] concreta para realizar el equilibrio de carga de una solicitud inicial. El valor predeterminado es **Basado en estado**, que asigna las solicitudes según el estado del servidor, tal y como se mide según la memoria disponible y la utilización del procesador. O bien, puede elegir **Operación por turnos** para asignar las solicitudes a los servidores en el mismo orden de repetición, con independencia de si un servidor está ocupado o inactivo.  
  
9. En Actualización de datos, en **Horario comercial**, puede especificar un intervalo de horas que defina un día laboral. Las programaciones de actualización de datos pueden ejecutarse al terminar un día laborable a fin de reunir los datos de las transacciones que se generaron durante las horas de trabajo normales.  
  
10. En **Cuenta de actualización de datos desatendida de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, puede especificar una aplicación de destino de Servicio de almacenamiento seguro predefinida que almacene una cuenta predefinida para ejecutar trabajos de actualización de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Asegúrese de especificar el nombre de la aplicación de destino y no el identificador. La aplicación de destino para la actualización de datos desatendida se crea automáticamente si utilizó la opción Nuevo servidor del programa de instalación de SQL Server con el objetivo de instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. De lo contrario, debe crear la aplicación de destino de forma manual. Para obtener instrucciones sobre cómo configurar la cuenta, vea [Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
11. En **Permitir a los usuarios especificar credenciales de Windows personalizadas**, puede activar o desactivar la casilla para especificar si los propietarios de programaciones pueden escribir credenciales de Windows arbitrarias para ejecutar una programación de la actualización de datos. Si activa esta casilla, la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] creará y administrará una aplicación de destino para cada conjunto de credenciales almacenadas. Para más información, vea [Configurar las credenciales almacenadas para la actualización de datos de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75).  
  
12. En **Longitud máxima de historial de procesamiento**, puede especificar cuánto tiempo conservar un registro histórico del procesamiento de la actualización de datos. Esta información aparece en las páginas del historial de actualización de datos que se mantienen para cada libro que usa la actualización de datos. También aparece en el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
13. En Recopilación de datos de uso, en **Intervalo de informe de consulta**, especifique un intervalo de tiempo para notificar las estadísticas de las consultas. Los estadísticas de las consulta se notifican como un único evento para reducir la comunicación entre servidores.  
  
14. En Historial de datos de uso, especifique cuánto tiempo mantener un registro histórico de los datos de uso. La información de uso aparece en el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Los informes serán menos efectivos si especifica un valor demasiado bajo para el historial de datos de uso.  
  
15. En Recopilación de datos de uso, en cada umbral de respuesta de las consultas, especifique un límite superior que determina dónde comienza una categoría y comienza otra. Estas categorías establecen una línea base con la que se mide el comportamiento de las consultas. Puede utilizar estas categorías para supervisar las tendencias en los tiempos de respuesta de las consultas de un sistema. Esta información aparece en el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
16. Haga clic en **Aceptar** para guardar los cambios.  
  
     Los cambios del tiempo de espera de la carga o del método de asignación solo se aplican a las nuevas solicitudes entrantes. Las solicitudes que ya están en curso están sujetas a los valores que estaban en vigor cuando se recibió la solicitud.  
  
##  <a name="AssignGSA"></a> Asignación de una aplicación de servicio PowerPivot a una aplicación web  
 Después de configurar una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede asignarla a una aplicación web agregándola a la lista de conexiones de aplicación de servicio de esa aplicación web. Hay dos formas de hacerlo:  
  
-   Agréguela al grupo de conexiones **Predeterminado** . El *grupo de conexiones predeterminado* es una colección de conexiones de aplicación de servicio que están disponibles para cualquier aplicación web que haga referencia a él. Debe agregar una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a esta lista.  
  
-   Cree una lista de conexiones **Personalizadas** para una aplicación web concreta. Si creó varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede elegir cuál utilizar seleccionándola en una lista personalizada.  
  
 El grupo de conexiones predeterminado aceptará más de una aplicación de servicio del mismo tipo. Con todo, tenga en cuenta que no se puede agregar más de una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a esta lista.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones web**.  
  
2.  Seleccione la aplicación para la que desea asignar una conexión (por ejemplo, SharePoint -80).  
  
3.  Haga clic en **Conexiones de servicio**.  
  
4.  En **Modificar el siguiente grupo de asociaciones**, seleccione **default** o **[custom]**.  
  
5.  En **[custom]**, active la casilla junto a las conexiones de aplicación de servicio que quiera usar. Si tiene varias aplicaciones de servicio de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicadas por el Tipo establecido en **Proxy de la aplicación de servicio PowerPivot**), elija solo una.  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="EditGSA"></a> Modificar las propiedades de la aplicación de servicio  
 Utilice las siguientes instrucciones para volver a abrir la página de propiedades que especifica el nombre de aplicación del servicio, el grupo de aplicaciones, la configuración de la base de datos y las asociaciones del servicio.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Seleccione la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , pero no haga clic en ella. Puede hacer clic en el nombre del tipo para seleccionar la fila completa.  
  
3.  Haga clic en **Propiedades** en la cinta de opciones.  
  
## <a name="see-also"></a>Vea también  
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  

