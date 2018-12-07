---
title: Trabajo con instantáneas (portal web) | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 9ae20556-e243-4a60-b076-9fd9e82c7355
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9cffd51ef8da35c7ee8c1e424c2cddbac92955cd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517281"
---
# <a name="working-with-snapshots-web-portal"></a>Trabajo con instantáneas (portal web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Para controlar si se van a crear instantáneas para un informe, haga clic en el botón de **puntos suspensivos (...)** de un informe, seleccione **Administrar** y **Almacenamiento en caché** o **Instantáneas del historial**.  
  
> [!NOTE]
> El servicio del Agente SQL Server debe estar iniciado.  
   
Puede crear una instantánea de caché para que las propiedades de ejecución específicas se ejecuten más rápido. También puede trabajar con instantáneas de historial para capturar diferentes momentos.  
  
## <a name="creating-a-cache-snapshot"></a>Crear una instantánea de almacenamiento en caché  
  
Haga esto para crear una instantánea.  
  
![ssRSWebPortal-report-caching4](../reporting-services/media/ssrswebportal-report-caching4.png)  
  
1.  En la página **Almacenamiento en caché** , seleccione **Ejecutar siempre este informe según las instantáneas generadas previamente** para habilitar las opciones para crear una instantánea.  
  
2.  Seleccione **Crear instantáneas de caché en un programa** si quiere programar una instantánea periódica. Si lo hace, puede usar una programación compartida o definir una programación personalizada para actualizar la instantánea.  
  
3.  Seleccione **Crear una instantánea de caché cuando haga clic en el botón Aplicar en esta página** si quiere crear una caché de instantánea ahora mismo. Si selecciona esta opción únicamente, la instantánea no se actualizará.  
  
## <a name="create-modify-and-delete-history-snapshots"></a>Crear, modificar y eliminar instantáneas del historial  
  
Para trabajar con instantáneas del historial, administre un informe y seleccione **Instantáneas del historial**.  
  
Use la página **Instantáneas del historial** para ver las instantáneas de informe que se han generado y almacenado a lo largo del tiempo. Según las opciones que se configuren en el servidor de informes, es posible que el historial solamente contenga las instantáneas más recientes.  
  
El historial del informe siempre se ve en el contexto del informe desde el que se origina. No se puede ver el historial de todos los informes de un servidor de informes en un solo lugar.  
  
Para generar una instantánea del historial, el informe debe poder ejecutarse en modo desatendido, es decir, hay que usar credenciales almacenadas; los informes parametrizados deben contener valores predeterminados para todos los parámetros. Un historial de informe se puede generar manualmente o como una operación programada. Las propiedades del historial en el informe determinan las formas en que se puede crear el historial.  
  
![ssRSWebPortal-historysnapshots1](../reporting-services/media/ssrswebportal-historysnapshots1.png)  
   
1.  Para crear una instantánea del historial, seleccione **+ Nueva instantánea del historial**. Esto hará que el informe se procese y se agregue una entrada a la lista.  
  
2.  Puede ir a la configuración para definir programaciones y políticas de retención.  
  
3.  Puede seleccionar una instantánea del historial para verla. Las instantáneas que aparecen en un historial de informe solamente se distinguen por la fecha y la hora en que fueron creadas. No hay manera de distinguir visualmente si una instantánea se generó como respuesta a una operación programada o manual.  
  
### <a name="schedule-and-settings"></a>Programación y configuración  
  
Si selecciona **Programación y configuración** , dispondrá de más opciones para la retención de programación y el control de instantáneas creadas.  
  
![ssRSWebPortal-historysnapshots2](../reporting-services/media/ssrswebportal-historysnapshots2.png)  
   
Opcionalmente, puede crear una programación para que las instantáneas se creen. También puede impedir que otras personas creen instantáneas. Si desactiva **Permitir que los usuarios puedan crear instantáneas de forma manual** , el botón **+ Nueva instantánea del historial**se deshabilitará.  
  
También puede definir cómo prefiere conservar las instantáneas.  
  
**Guardar también las instantáneas de caché en el historial de informes**  
  
Si activa esta casilla, se copiará en el historial de un informe una instantánea del informe generada según las propiedades de ejecución del informe. Puede establecer las propiedades de ejecución de informes para ejecutar un informe a partir de una instantánea generada. Al establecer esta propiedad del historial del informe, se puede mantener un registro de todas las instantáneas del informe generadas con el tiempo, colocando copias de las mismas en el historial.

## <a name="next-steps"></a>Pasos siguientes

[Portal web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabajo con informes paginados](working-with-paginated-reports-web-portal.md)  
[Trabajo con conjuntos de datos compartidos](../reporting-services/work-with-shared-datasets-web-portal.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
