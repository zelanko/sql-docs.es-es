---
title: Crear y configurar una aplicación de servicio PowerPivot en Administración Central | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 64997cb3db784ea78a72a7c812c8f88034c2358d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071582"
---
# <a name="create-and-configure-a-powerpivot-service-application-in-central-administration"></a>Crear y configurar una aplicación de servicio PowerPivot en Administración central
  Una aplicación de servicio PowerPivot es una instancia de servicio compartido del servicio de sistema de PowerPivot. Cada aplicación de servicio tiene su propia identidad de aplicación, configuración, propiedades y almacenamiento de datos interno.  
  
 Este tema contiene las siguientes secciones:  
  
 [Determinar si se debe crear una nueva aplicación de servicio PowerPivot](#determine)  
  
 [Crear una aplicación de servicio PowerPivot](#CreateApp)  
  
 [Configurar la aplicación de servicio PowerPivot](#ConfigApp)  
  
 [Asignación de una aplicación de servicio PowerPivot a una aplicación Web](#AssignGSA)  
  
 [Modificar las propiedades de la aplicación de servicio](#EditGSA)  
  
##  <a name="determine"></a> Determinar si se debe crear una nueva aplicación de servicio PowerPivot  
 Una instalación de PowerPivot para SharePoint debe tener al menos una aplicación de servicio PowerPivot en la granja. Una aplicación de servicio se crea automáticamente si utilizó la Herramienta de configuración de PowerPivot para configurar el servidor. Si no, debe crear una aplicación de servicio PowerPivot manualmente en Administración central.  
  
 Al crear una aplicación de servicio, el servicio estará disponible y se generará la base de datos de aplicación del servicio. En función de las opciones que seleccione al crear la aplicación de servicio, se agregará una conexión de servicio PowerPivot al grupo de conexiones de servicio predeterminado. Todas las aplicaciones web de SharePoint que se suscriban al grupo de conexiones de servicio predeterminado obtendrán automáticamente acceso inmediato a la aplicación de servicio PowerPivot.  
  
 Puede crear varias aplicaciones de servicio PowerPivot. Aunque una aplicación de servicio es suficiente en la mayoría de los escenarios de implementación, podría considerar la creación de una aplicación de servicio PowerPivot adicional si entre los requisitos corporativos se hallan los siguientes:  
  
-   Usar una cuenta de actualización de datos PowerPivot desatendida diferente para cada aplicación.  
  
-   Usar distintos tiempos de espera, historial de uso y umbrales para los informes de respuesta de las consultas.  
  
-   Delegar la administración del servicio a distintas personas. Un administrador verá el historial de la actualización de datos, los datos de uso y otras propiedades solo para la aplicación que administra. Si tiene que aislar las aplicaciones web de SharePoint (por ejemplo, si su empresa es un servicio de hospedaje que debe garantizar el aislamiento de los datos para las aplicaciones web de SharePoint que pertenecen a distintos clientes), crear aplicaciones de servicio PowerPivot separadas puede ayudar a cumplir los requisitos de aislamiento, porque garantiza que cada administrador de servicio ve solo la configuración y las propiedades de la aplicación que administra.  
  
 La creación de aplicaciones de servicio adicionales introduce nuevos requisitos para administrar las asociaciones del servicio. Sería necesario que creara y usara listas de asociaciones de servicios personalizadas para cada aplicación de servicio adicional que cree.  
  
 Si no tiene una razón concreta para crear una aplicación de servicio PowerPivot más, debería utilizar solo una para todas las aplicaciones web de la granja.  
  
##  <a name="CreateApp"></a> Crear una aplicación de servicio PowerPivot  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta **Aplicaciones de servicio** , haga clic en **Nuevo**.  
  
3.  Seleccione **aplicación de servicio PowerPivot SQL Server**. Si no aparece en la lista, PowerPivot para SharePoint no se instaló o configuró correctamente.  
  
4.  En el **crear nueva aplicación de servicio de PowerPivot** , escriba un nombre para la aplicación. El valor predeterminado es PowerPivotServiceApplication\<número >. Si va a crear varias aplicaciones de servicio PowerPivot, un nombre descriptivo ayudará a otros administradores a saber cómo se utiliza la aplicación.  
  
5.  En Grupo de aplicaciones, cree un nuevo grupo de aplicaciones para la aplicación (recomendado). Seleccione o cree una cuenta administrada para el grupo de aplicaciones. No olvide especificar una cuenta de usuario de dominio. Una cuenta de usuario de dominio habilita el uso de la característica de cuentas administradas de SharePoint, que permite actualizar la información de cuentas y contraseñas en un solo lugar. Las cuentas de dominio también se necesitan si planea escalar la horizontalmente la implementación para incluir instancias de servicio adicionales que se ejecutarán bajo la misma identidad.  
  
6.  En **Servidor de bases de datos**, el valor predeterminado es la instancia del motor de base de datos de SQL Server que hospeda las bases de datos de configuración de la granja. Puede utilizar este servidor o elegir un servidor SQL Server diferente.  
  
7.  En **nombre de base de datos**, el valor predeterminado es PowerPivotServiceApplication1_\<guid >. Debe crear una base de datos única para cada aplicación de servicio PowerPivot. El nombre predeterminado de la base de datos corresponde al de la aplicación de servicio. Si escribió un nombre de aplicación del servicio único, siga una convención de nomenclatura similar para el nombre de la base de datos, de modo que pueda administrarlos juntos.  
  
8.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige **Autenticación de SQL**, consulte la guía del administrador de SharePoint para obtener información sobre cómo usar este tipo de autenticación en una implementación de SharePoint.  
  
9. Si lo desea, seleccione la casilla de verificación **agregar el proxy para esta aplicación de servicio PowerPivot al grupo de proxy de la granja de servidores de forma predeterminada.** De esta forma se agrega la conexión de la aplicación de servicio al grupo de conexiones de servicio predeterminado.  
  
     Debe activar esta casilla si está creando la primera aplicación de servicio PowerPivot. Debe haber una aplicación de servicio PowerPivot en el grupo de conexiones predeterminado para que el Panel de administración de PowerPivot funcione correctamente.  
  
     No agregue la aplicación de servicio PowerPivot al grupo de conexiones predeterminado si ya hay una. Agregar varias entradas del mismo tipo de aplicación de servicio no se admite y podría producir errores. Si está creando aplicaciones de servicio adicionales, déjelas fuera del grupo de conexiones predeterminado y agréguelas a listas personalizadas.  
  
     Para obtener más información acerca de las asociaciones de servicio, consulte [conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en Administración Central](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Haga clic en **Aceptar.** La aplicación de servicio aparecerá junto a otros servicios administrados en la lista de aplicaciones de servicio de la granja.  
  
##  <a name="ConfigApp"></a> Configurar la aplicación de servicio PowerPivot  
 Una aplicación de servicio PowerPivot se crea utilizando una configuración predeterminada. La configuración predeterminada se recomienda en la mayoría de los escenarios. Cámbiela únicamente si encuentra que el tiempo de respuesta es lento o que se quitan conexiones, o si va a variar la configuración de servicio PowerPivot para aplicaciones web de SharePoint concretas.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
     En la lista de aplicaciones de servicio, debería ver la aplicación de servicio que ha creado y denominado. El valor predeterminado es **PowerPivotServiceApplication1**.  
  
2.  Haga clic en la aplicación de servicio PowerPivot. Así se abre el panel de administración de PowerPivot.  
  
3.  En la lista **Acciones** en la esquina superior derecha del panel, haga clic en **Configurar las opciones de aplicación de servicio**.  
  
4.  En **el tiempo de espera de base de datos de carga**, aumente o disminuya el valor para cambiar cuánto tiempo el servicio PowerPivot espera una respuesta de la instancia de SQL Server Analysis Services (PowerPivot) a la que reenvió una solicitud de carga de datos. Dado que los conjuntos de datos muy grandes tardan tiempo en atravesar la conexión, debe permitir el tiempo suficiente para que la instancia de servicio PowerPivot recupere el libro de Excel y mueva los datos PowerPivot a una instancia de Analysis Services para el procesamiento de consultas. Dado que los datos PowerPivot pueden ser extraordinariamente grandes, el valor predeterminado es de 30 minutos.  
  
5.  En **Tiempo de espera del grupo de conexiones**, aumente o disminuya el valor para cambiar el número de minutos que una conexión de datos inactiva permanecerá abierta. El valor predeterminado es de 30 minutos. Durante este período, el servicio PowerPivot reutilizará una conexión de datos inactiva para las solicitudes de solo lectura en el mismo usuario de SharePoint para los mismos datos PowerPivot. Si no se reciben más solicitudes para esos datos durante el período especificado, la conexión se quita del conjunto. Los valores válidos van de 1 a 3600 segundos. Para obtener más información acerca de los grupos de conexión, consulte [referencia de las opciones configuración &#40;PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md).  
  
6.  En **máximo tamaño de grupo de conexiones de usuario**, aumente o disminuya el valor para cambiar el número máximo de conexiones inactivas que el servicio PowerPivot creará en grupos de conexiones individuales para cada usuario de SharePoint, conjunto de datos de PowerPivot y combinaciones de versión.  
  
     El valor predeterminado es de 1000 conexiones inactivas. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de usuario), o de 1 a 10000.  
  
     Estos grupos de conexiones permiten al servicio admitir más eficazmente conexiones continuadas a los mismos datos de solo lectura del mismo usuario. Si deshabilita la agrupación de conexiones, cada conexión se creará como nueva.  
  
     Observe que cambiar el límite del tamaño del grupo de conexiones, incluso si se establece en 0, no hará que se quiten conexiones. Los grupos de conexiones existen para reducir los tiempos de espera al conectar a los datos. El servicio PowerPivot nunca denegará una conexión según la configuración del grupo de conexiones.  
  
7.  En **máximo tamaño de grupo de conexiones administrativas**, aumente o disminuya el valor para cambiar el número de conexiones abiertas en un grupo de conexiones creado para una conexión de servicio PowerPivot a Analysis Services. Cada instancia de servicio PowerPivot abre una conexión administrativa independiente a la instancia de Analysis Services en el mismo equipo. El servicio PowerPivot crea un conjunto independiente para reutilizar las conexiones administrativas con el propósito de comprobar si hay conexiones inactivas y supervisar el estado del servidor. El valor predeterminado es de 200 conexiones. Los valores válidos son -1 (ilimitado), 0 (deshabilita la agrupación de conexiones de administrador), o de 1 a 10.000. Si selecciona 0, cada conexión se creará como nueva.  
  
8.  En **método de asignación**, puede especificar el esquema que el servicio de sistema de PowerPivot se utiliza para seleccionar una aplicación de servicio PowerPivot concreta para una solicitud inicial de equilibrio de carga de equilibrio de carga. El valor predeterminado es **Basado en estado**, que asigna las solicitudes según el estado del servidor, tal y como se mide según la memoria disponible y la utilización del procesador. O bien, puede elegir **Operación por turnos** para asignar las solicitudes a los servidores en el mismo orden de repetición, con independencia de si un servidor está ocupado o inactivo.  
  
9. En Actualización de datos, en **Horario comercial**, puede especificar un intervalo de horas que defina un día laboral. Las programaciones de actualización de datos pueden ejecutarse al terminar un día laborable a fin de reunir los datos de las transacciones que se generaron durante las horas de trabajo normales.  
  
10. En **cuenta de la actualización de datos desatendida de PowerPivot**, puede especificar una aplicación de destino el servicio Store seguro predefinida que almacene una cuenta predefinida para ejecutar trabajos de actualización de datos de PowerPivot. Asegúrese de especificar el nombre de la aplicación de destino y no el identificador. La aplicación de destino para la actualización de datos desatendida se crea automáticamente si utilizó la opción Nuevo servidor del programa de instalación de SQL Server para instalar PowerPivot para SharePoint. De lo contrario, debe crear la aplicación de destino de forma manual. Para obtener instrucciones sobre cómo configurar la cuenta, consulte [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
11. En **Permitir a los usuarios especificar credenciales de Windows personalizadas**, puede activar o desactivar la casilla para especificar si los propietarios de programaciones pueden escribir credenciales de Windows arbitrarias para ejecutar una programación de la actualización de datos. Si activa esta casilla, la aplicación de servicio PowerPivot creará y administrará una aplicación de destino para cada conjunto de credenciales almacenadas. Para obtener más información, consulte [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
12. En **Longitud máxima de historial de procesamiento**, puede especificar cuánto tiempo conservar un registro histórico del procesamiento de la actualización de datos. Esta información aparece en las páginas del historial de actualización de datos que se mantienen para cada libro que usa la actualización de datos. También aparece en el Panel de administración de PowerPivot.  
  
13. En Recopilación de datos de uso, en **Intervalo de informe de consulta**, especifique un intervalo de tiempo para notificar las estadísticas de las consultas. Los estadísticas de las consulta se notifican como un único evento para reducir la comunicación entre servidores.  
  
14. En Historial de datos de uso, especifique cuánto tiempo mantener un registro histórico de los datos de uso. La información de uso aparece en el Panel de administración de PowerPivot. Los informes serán menos efectivos si especifica un valor demasiado bajo para el historial de datos de uso.  
  
15. En Recopilación de datos de uso, en cada umbral de respuesta de las consultas, especifique un límite superior que determina dónde comienza una categoría y comienza otra. Estas categorías establecen una línea base con la que se mide el comportamiento de las consultas. Puede utilizar estas categorías para supervisar las tendencias en los tiempos de respuesta de las consultas de un sistema. Esta información aparece en el Panel de administración de PowerPivot.  
  
16. Haga clic en **Aceptar** para guardar los cambios.  
  
     Los cambios del tiempo de espera de la carga o del método de asignación solo se aplican a las nuevas solicitudes entrantes. Las solicitudes que ya están en curso están sujetas a los valores que estaban en vigor cuando se recibió la solicitud.  
  
##  <a name="AssignGSA"></a> Asignación de una aplicación de servicio PowerPivot a una aplicación Web  
 Después de configurar una aplicación de servicio PowerPivot, puede asignarla a una aplicación web agregándola a la lista de conexiones de aplicación de servicio de esa aplicación web. Hay dos formas de hacerlo:  
  
-   Agréguela al grupo de conexiones **Predeterminado** . El *grupo de conexiones predeterminado* es una colección de conexiones de aplicación de servicio que están disponibles para cualquier aplicación web que haga referencia a él. Debe agregar una aplicación de servicio PowerPivot a esta lista.  
  
-   Cree una lista de conexiones **Personalizadas** para una aplicación web concreta. Si creó varias aplicaciones de servicio PowerPivot, puede elegir cuál utilizar seleccionándola en una lista personalizada.  
  
 El grupo de conexiones predeterminado aceptará más de una aplicación de servicio del mismo tipo. Con todo, tenga en cuenta que no se puede agregar más de una aplicación de servicio PowerPivot a esta lista.  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones web**.  
  
2.  Seleccione la aplicación para la que desea asignar una conexión (por ejemplo, SharePoint -80).  
  
3.  Haga clic en **Conexiones de servicio**.  
  
4.  En **Modificar el siguiente grupo de asociaciones**, seleccione **default** o **[custom]**.  
  
5.  En **[custom]**, active la casilla junto a las conexiones de aplicación de servicio que quiera usar. Si tiene varias aplicaciones de servicio PowerPivot (indicado por el tipo establecido en `PowerPivot Service Application Proxy`), asegúrese de elegir solo uno.  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="EditGSA"></a> Modificar las propiedades de la aplicación de servicio  
 Utilice las siguientes instrucciones para volver a abrir la página de propiedades que especifica el nombre de aplicación del servicio, el grupo de aplicaciones, la configuración de la base de datos y las asociaciones del servicio.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Seleccione la aplicación de servicio PowerPivot, pero no haga clic en ella. Puede hacer clic en el nombre del tipo para seleccionar la fila completa.  
  
3.  Haga clic en **Propiedades** en la cinta de opciones.  
  
## <a name="see-also"></a>Vea también  
 [Administración y configuración del servidor PowerPivot en Administración central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
