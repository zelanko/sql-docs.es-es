---
title: Programar una actualización de datos (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 8571208f-6aae-4058-83c6-9f916f5e2f9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b2840a8c4f756ce26c5e915af6860929354bae3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178465"
---
# <a name="schedule-a-data-refresh-powerpivot-for-sharepoint"></a>Programar una actualización de datos (PowerPivot para SharePoint)
  Puede programar la actualización de datos para obtener actualizaciones automáticas de los datos PowerPivot dentro de un libro de Excel que publicara en un sitio de SharePoint.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
 **En este tema:**  
  
 [Requisitos previos](#prereq)  
  
 [Información general sobre la actualización de datos](#intro)  
  
 [Habilitar y programar la actualización de datos](#drenablesched)  
  
 [Comprobar la actualización de datos](#drverify)  
  
> [!NOTE]  
>  Las instancias de servidor de Analysis Services realizan la actualización de los datos PowerPivot en la granja de servidores de SharePoint. No está relacionada con la característica de actualización de datos que se proporciona en Excel Services. La característica de programación de actualizaciones de datos de PowerPivot no actualizará los datos que no sean de PowerPivot.  
  
##  <a name="prereq"></a> Requisitos previos  
 Debe tener el nivel de permisos para contribuir o uno superior en el libro si desea crear una programación para la actualización de datos.  
  
 Los orígenes de datos externos a los que se tiene acceso durante la actualización de datos deben estar disponibles y las credenciales que especifique en la programación deben tener el permiso de acceso a esos orígenes de datos. La actualización de datos programada requiere la ubicación de un origen de datos que sea accesible a través de una conexión de red (por ejemplo, desde un recurso compartido de archivos de red en lugar de una carpeta local en la estación de trabajo).  
  
 El origen de datos no puede ser un documento de Office ni una base de datos de Access. Office no admite el uso de los componentes de conectividad de Office en un entorno de servidor. Si el libro contiene datos de estos orígenes, asegúrese de quitar esos orígenes de la lista de orígenes de datos en la programación de actualización de datos.  
  
 El libro debe ser una versión de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Si usa los libros creados en la versión anterior de PowerPivot para Excel, la actualización de datos de la programación no funcionará a menos que actualice la base de datos a la nueva versión.  
  
 El libro se debe proteger en el momento en que la operación de actualización finalice. Para ello, una vez finalizada la actualización de los datos, se realiza un bloqueo del libro del archivo. Este bloqueo se ejecuta cuando se guarda el archivo, y no cuando se inicia la actualización.  
  
> [!NOTE]  
>  El servidor no bloquea el libro mientras la actualización de datos esté en curso. Sin embargo, bloquea el archivo al final de la actualización de datos con el fin de proteger el archivo actualizado. Si, en este momento, el archivo se desprotege para otro usuario, los datos actualizados se eliminarán. De igual modo, si el archivo está protegido, pero es significativamente diferente de la copia recuperada por el servidor al comenzar la actualización de datos, los datos actualizados se descartarán.  
  
##  <a name="intro"></a> Información general sobre la actualización de datos  
 Los datos PowerPivot de libro de Excel pueden originarse en varios orígenes de datos externos como son bases de datos externas o archivos de datos a los que tiene acceso desde servidores remotos o desde recursos compartidos de archivos de red. En el caso de libros PowerPivot que contengan datos importados de orígenes de datos externos o conectados, puede configurar la actualización de datos para programar una importación automática de los datos actualizados de esos orígenes iniciales.  
  
 El acceso a un origen de datos externo se obtiene a través de una dirección URL, ruta UNC o cadena de conexión incrustada que se especifica al importar los datos originales en el libro utilizando la aplicación cliente de PowerPivot. La información de conexión original que está almacenada en el libro PowerPivot se reutiliza para las operaciones de actualización de datos subsiguientes. Aunque puede sobrescribir las credenciales que se usan para conectarse a los orígenes de datos, no puede sobrescribir las cadenas de conexión para la actualización de datos; solo se utiliza la información de conexión existente.  
  
 Solo hay una página de programación de actualización de datos para cada libro y toda la información de programación se especifica en esa página. Normalmente, la persona que creó el libro define la programación.  
  
 Como propietario de la programación, realice las siguientes tareas:  
  
-   Defina la programación predeterminada. Esta es la programación que se utiliza si no hay ninguna programación definida en el nivel del origen de datos.  
  
-   Especifique las credenciales que se van a usar para ejecutar la actualización de los datos.  
  
-   Elija los orígenes de datos que se van a incluir en la operación de actualización.  
  
-   Si lo desea, puede especificar también programaciones específicas en línea y las credenciales de cada origen de datos que se va a consultar durante la actualización de datos. Cada origen de datos se puede actualizar de forma independiente. Si crea programaciones personalizadas para cada origen de datos, se omitirá la programación predeterminada.  
  
 Al crear programaciones específicas para orígenes de datos individuales se permite hacer coincidir la programación de la actualización con las fluctuaciones en los orígenes de datos externos. Por ejemplo, si un origen de datos externo contiene datos transaccionales que se generan a lo largo del día, puede crear una programación individual de la actualización de datos para que ese origen de datos obtenga su información actualizada por la noche.  
  
##  <a name="drenablesched"></a> Habilitar y programar la actualización de datos  
 Utilice las siguientes instrucciones para programar la actualización de datos para los datos PowerPivot en un libro de Excel que esté publicado en una biblioteca de SharePoint.  
  
1.  En la biblioteca que contenga el libro, selecciónelo y, a continuación, haga clic en la flecha abajo para mostrar una lista de comandos.  
  
2.  Haga clic en **Administrar actualización de datos PowerPivot**. Si ya se ha definido una programación de actualización de datos, en su lugar verá la página del historial para ver la actualización de datos. Puede hacer clic en **Configurar actualización de datos** para abrir la página de definición de la programación.  
  
3.  En la página de definición de la programación, active la casilla **Habilitar** .  
  
4.  En Detalles de programación, especifique el tipo de programación y sus detalles. En este paso se crea la programación predeterminada.  
  
    > [!IMPORTANT]  
    >  Asegúrese de activar la casilla **También actualizar lo más rápido posible** . Esto le permite comprobar que la actualización de datos funciona para este libro. Tenga en cuenta que una vez guardada la programación, puede tardar hasta un minuto el inicio de la actualización de datos.  
  
5.  En Hora de inicio más temprana, elija una de las siguientes:  
  
    1.  **Después del horario comercial** especifica un período de procesamiento fuera del horario comercial cuando es más probable que los servidores de bases de datos tengan los datos actuales que se generaron a lo largo del día laboral.  
  
    2.  **Hora de inicio más temprana específica** es la hora y los minutos de la hora más cercana del día en que le gustaría que la solicitud de actualización de datos se agregara a una cola de procesos. Los minutos se pueden especificar en intervalos de 15 minutos. La configuración se aplica al día actual así como a fechas futuras. Por ejemplo, si especifica el valor 6:30 a.m. y la hora actual son las 4:30 p.m., la solicitud de actualización se agregará a la cola en el día actual porque 4:30 p.m. es después de las 6:30 a.m.  
  
     La hora de inicio más temprana define cuándo se agrega una solicitud a la cola de procesos. El procesamiento real se produce cuando el servidor tiene los recursos adecuados para comenzar el procesamiento de los datos. El tiempo de procesamiento real se registrará en el historial de la actualización de datos una vez completado el procesamiento.  
  
6.  Active la casilla **También actualizar lo más rápido posible** para ejecutar la actualización de datos en cuanto el servidor pueda procesarla. Un resultado correcto de un trabajo de actualización de datos comprueba que los orígenes de datos disponibles y que los permisos y la configuración de servidor están establecidos correctamente.  
  
7.  En Notificaciones de correo electrónico, escriba la dirección de correo electrónico de la persona a la que se debería notificar en caso de un error de procesamiento.  
  
8.  En Credenciales, especifique una cuenta utilizada para ejecutar el trabajo de actualización de datos. La cuenta debe tener permisos para contribuir en el libro y poder abrirlo y actualizar sus datos. Debe ser una cuenta de usuario de dominio de Windows. En muchos casos, esta cuenta también debe tener permisos de lectura en los orígenes de datos externos utilizados durante la actualización de datos. En concreto, si importó originalmente los datos mediante la opción Utilizar autenticación de Windows, la cadena de conexión se genera para utilizar las credenciales de Windows del usuario actual. Si el usuario actual es la cuenta de actualización de datos, la cuenta debe tener permisos de lectura en el origen de datos externo para que la actualización de datos se realice correctamente. Elija una de las opciones siguientes:  
  
    1.  Elija **Usar la cuenta de actualización de datos configurada por el administrador** para procesar la operación de actualización de datos mediante la cuenta de actualización de datos desatendida de PowerPivot.  
  
    2.  Elija **Conectar con las siguientes credenciales de usuario de Windows** si desea escribir un nombre de usuario y contraseña. Escriba la información de la cuenta con el formato dominio\usuario.  
  
    3.  Elija **Conectar con las credenciales guardadas en el Servicio de almacenamiento seguro** si conoce el identificador de una aplicación de destino que contenga las credenciales almacenadas previamente que desea utilizar.  
  
     Para obtener más información acerca de estas opciones, consulte [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41; ](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md) y [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
9. En Orígenes de datos, active la casilla **Todos los orígenes de datos** si desea que la actualización de datos vuelva a consultar todos los orígenes de datos originales.  
  
     Si selecciona esta opción, cualquier origen de datos externo que proporcione los datos PowerPivot se incluye automáticamente en la actualización, aun cuando la lista de orígenes de datos cambie con el tiempo a medida que agregue o quite los orígenes de datos que proporcionan datos al libro.  
  
     Desactive la casilla **Todos los orígenes de datos** si desea seleccionar manualmente qué orígenes de datos incluir. Si posteriormente modifica el libro agregando un nuevo origen de datos, asegúrese de actualizar la lista de orígenes de datos en la programación. De lo contrario, los orígenes de datos más recientes no se incluirán en la operación de actualización.  
  
     La lista de orígenes de datos entre los que puede elegir se recupera del libro PowerPivot al abrir la página Administrar actualización de datos PowerPivot para el libro.  
  
     Asegúrese de seleccionar solo los orígenes de datos que cumplan los siguientes criterios:  
  
    -   El origen de datos debe estar disponible en la ubicación indicada en el momento en que se produce la actualización de datos. Si el origen de datos original está en una unidad de disco local del usuario que creó el libro, debe excluir ese origen de datos de la operación de actualización de datos o encontrar una manera de publicarlo en una ubicación que sea accesible a través de una conexión de red. Si mueve un origen de datos a una ubicación de red, asegúrese de abrir el libro en [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] y actualice la información de conexión del origen de datos. Esto es necesario para restablecer la información de conexión que está almacenada en el libro PowerPivot.  
  
    -   Se debe tener acceso al origen de datos utilizando la información de credenciales que está insertada en el libro PowerPivot o que se haya especificado en la programación. La información de credenciales insertadas se almacena en el libro PowerPivot al importar los datos con PowerPivot para Excel. La información de credenciales insertada suele ser SSPI=IntegratedSecurity o SSPI=TrustedConnection, lo que significa que las credenciales del usuario actual se usan para conectarse al origen de datos. Si desea invalidar la información de credenciales en la programación de actualización de datos, puede especificar credenciales predefinidas almacenadas. Para obtener más información, consulte [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
    -   La actualización de datos debe realizarse para todos los orígenes de datos que especifique. De lo contrario, se descartan los datos actualizados y se queda con la última versión guardada del libro. Excluya cualquier origen de datos en el que no confíe completamente.  
  
    -   La actualización de datos no debe invalidar otros datos del libro. Al actualizar un subconjunto de los datos, es importante que sepa si el libro es válido aún una vez se agreguen nuevos datos con datos estáticos que no sean del mismo período. Como autor de un libro, es su responsabilidad conocer sus dependencia de datos y asegurarse de que la actualización de datos es adecuada para el propio libro.  
  
10. Opcionalmente, puede definir programaciones individuales para orígenes de datos concretos. Esto es útil si tiene orígenes de datos originales que se actualicen a sí mismos según una programación. Por ejemplo, si un origen de datos PowerPivot utiliza los datos de un data mart que se actualiza todos los lunes a las 02:00 horas, puede definir una programación incorporada para que el data mart recupere sus datos actualizados todos los lunes a las 04:00 horas.  
  
11. Haga clic en **Aceptar** para guardar la programación.  
  
##  <a name="drverify"></a> Comprobar la actualización de datos  
 La mejor forma de comprobar la actualización de datos es ejecutarla inmediatamente y revisar la página del historial para ver si se completó de modo correcto. Al activar la casilla **También actualizar lo más rápido posible** en la programación se comprobará que la actualización de datos está operativa.  
  
 Puede ver el registro actual y pasado de las operaciones de actualización de datos en la página Historial de actualización de datos para el libro. Esta página solo aparece si la actualización de datos se ha programado para un libro. Si no hay ninguna programación de actualización de datos, la página de definición de la programación aparece en su lugar.  
  
 Debe tener permisos para contribuir u otros superiores para ver el historial de la actualización de datos.  
  
1.  En un sitio de SharePoint, abra la biblioteca que contiene un libro PowerPivot.  
  
     No hay ningún indicador visual que identifique qué libros en una biblioteca de SharePoint contienen datos PowerPivot. Debe saber de antemano qué libros contienen los datos PowerPivot actualizables.  
  
2.  Seleccione el documento y, a continuación, haga clic en la flecha abajo que aparece a la derecha.  
  
3.  Seleccione **Administrar actualización de datos PowerPivot**.  
  
 Aparece la página del historial y muestra un registro completo de toda la actividad de actualización de los datos PowerPivot en el libro de Excel actual, incluido el estado de la operación de actualización de datos más reciente.  
  
 En algunos casos, podría ver que los tiempos de procesamiento reales difieren del tiempo que especificó. Esto ocurrirá si hay mucha carga de procesamiento en el servidor. Con mucha carga, la instancia de servicio de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] esperará a que se liberen suficientes recursos del sistema antes de comenzar una actualización de datos.  
  
 El libro se debe proteger en el momento en que la operación de actualización finalice. El libro se guardará con los datos actualizados en ese momento. Si se desprotege el archivo, la actualización de datos se omite hasta el siguiente período programado.  
  
 Si ve un mensaje de estado inesperado (por ejemplo, que informa acerca de un error o de la cancelación de la operación de actualización), puede investigar el problema comprobando los permisos y la disponibilidad del servidor.  
  
 Revise la página de solución de problemas de actualización de datos PowerPivot en el WIKI de TechNet de ayuda para resolver problemas de actualización de datos. Para obtener más información vea [Solucionar problemas de la actualización de datos PowerPivot](http://go.microsoft.com/fwlink/?LinkId=251594).  
  
> [!NOTE]  
>  Los administradores de SharePoint pueden ayudarle a solucionar los problemas de la actualización de datos viendo los informes de la actualización de datos consolidados en el Panel de administración de PowerPivot en Administración central. Para obtener más información, consulte [PowerPivot Management Dashboard and Usage Data](power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Vea también  
 [Actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Ver historial de actualización de datos &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)   
 [Configurar credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
