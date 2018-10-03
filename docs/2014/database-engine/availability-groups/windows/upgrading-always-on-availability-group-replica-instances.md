---
title: Actualización de los servidores del grupo de disponibilidad con una pérdida de datos y tiempo de inactividad mínimo y de actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 640a1af48b83474cbeb331268fd4cf1ab808995b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155965"
---
# <a name="upgrade-and-update-of-availability-group-servers-with-minimal-downtime-and-data-loss"></a>Actualizar servidores de un grupo de disponibilidad con una pérdida de datos y un tiempo de inactividad mínimos
  Al actualizar instancias de servidor de SQL Server 2012 a un Srvice Pack o una versión más reciente, puede reducir el tiempo de inactividad de un grupo de disponibilidad a solo una conmutación por error manual realizando una actualización secuencial. La actualización de las versiones de SQL Server se conoce como adaptación (upgrade) gradual; la actualización de la versión actual de SQL Server con revisiones o Service Packs se conoce como actualización (update) gradual.  
  
 Este tema limita la explicación únicamente a las adaptaciones y a las actualizaciones de SQL Server (a las que, de aquí en adelante, se hará referencia genéricamente como actualizaciones). Para relacionados con el sistema operativo actualizaciones de que se ejecutan las instancias de SQL Server de alta disponibilidad en, consulte [entre clústeres migración de grupos de disponibilidad AlwaysOn para las actualizaciones del sistema operativo](http://msdn.microsoft.com/library/jj873730.aspx)  
  
## <a name="rolling-upgradeupdate-best-practices-for-alwayson-availability-groups"></a>Prácticas recomendadas de las actualizaciones graduales en grupos de disponibilidad AlwasysOn  
 Las siguientes prácticas recomendadas deberían observarse al realizar actualizaciones de servidor a fin de reducir el tiempo de inactividad y la pérdida de datos en los grupos de disponibilidad:  
  
-   Antes de comenzar la actualización gradual,  
  
    -   Realice una conmutación por error manual de prueba en al menos una de réplicas de confirmación sincrónica  
  
    -   Proteja los datos realizando una copia de seguridad de la base de datos completa en cada base de datos de disponibilidad  
  
    -   Ejecute DBCC CHECKDB en cada base de datos de disponibilidad  
  
-   Actualice siempre los nodos de las réplicas secundarias remotas, después los de las locales y, a continuación, el nodo de la réplica principal en último lugar.  
  
-   No se pueden realizar copias de seguridad de una base de datos que se está actualizando.  Antes de actualizar las réplicas secundarias, configure la preferencia de copia de seguridad automatizada para ejecutar las copias de seguridad solo en la réplica principal.  Antes de actualizar la réplica principal, modifique esta configuración para ejecutar las copias de seguridad solo en las réplicas secundarias.  
  
-   Para impedir las conmutaciones por error no intencionadas del grupo de disponibilidad durante el proceso de actualización, quite la conmutación por error de disponibilidad de las réplicas de confirmación sincrónica antes de comenzar.  
  
-   No actualice el nodo de la réplica principal antes de conmutar por error el grupo de disponibilidad a un nodo actualizado con una réplica secundaria en primer lugar. De lo contrario, las aplicaciones cliente pueden sufrir un tiempo de inactividad ampliado durante la actualización en la réplica principal.  
  
-   Conmute por error el grupo de disponibilidad siempre a un nodo de una réplica secundaria de confirmación sincrónica. Si conmuta por error a una réplica secundaria de confirmación asincrónica, las bases de datos sufrirán la pérdida de datos y el movimiento de datos se suspende automáticamente hasta que reanude de forma manual el movimiento de datos.  
  
-   No actualice el nodo de la réplica principal antes de actualizar cualquier otro nodo de una réplica secundaria. Una réplica principal actualizada ya no puede entregar registrar a ninguna réplica secundaria que aún no haya sido actualizada a la misma versión. Cuando el movimiento de datos a una réplica secundaria se suspenda, no puede producirse la conmutación por error automática para dicha réplica y las bases de datos de disponibilidad son vulnerables ante la pérdida de datos.  
  
-   Ante de conmutar por error un grupo de disponibilidad, compruebe que el estado de sincronización del destino de la conmutaicón es SINCRONIZADO.  
  
## <a name="rolling-upgradeupdate-process"></a>Proceso de actualización gradual  
 En la práctica, el proceso exacto dependerá de factores como la topología de implementación de los grupos de disponibilidad y del modo de confirmación de cada réplica. Pero, en un escenario más sencillo, una actualización gradual es un proceso de varias fases que en su forma más sencilla implica los pasos siguientes:  
  
 ![Actualización de un grupo de disponibilidad en un escenario de HADR](../../media/alwaysonupgrade-ag-hadr.gif "Actualización de un grupo de disponibilidad en un escenario de HADR")  
  
1.  Quitar la conmutación por error automática en todas las réplicas de confirmación sincrónica  
  
2.  Actualizar todas las instancias de servidor remoto que ejecutan réplicas secundarias de confirmación asincrónica  
  
3.  Actualizar todas las instancias de servidor local que no se ejecutan actualmente en la réplica principal  
  
4.  Conmutar por error el grupo de disponibilidad de forma manual a una réplica secundaria de confirmación sincrónica  
  
5.  Actualizar la instancia de servidor que antes hospedaba la réplica principal  
  
6.  Configurar los asociados de conmutación por error automática según convenga  
  
 Si es necesario, puede realizar una conmutación por error manual adicional para devolver al grupo de disponibilidad a su configuración original.  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>Grupo de disponibilidad con una réplica secundaria remota  
 Si ha implementado un grupo de disponibilidad para la recuperación de desastres, puede que tenga que conmutar por error el grupo de disponibilidad a una réplica secundaria de confirmación asincrónica. Tal configuración se muestra en la ilustración siguiente:  
  
 ![Actualización de un grupo de disponibilidad en un escenario de DR](../../media/agupgrade-ag-dr.gif "Actualización de un grupo de disponibilidad en un escenario de DR")  
  
 En esta situación, debe conmutar por error el grupo de disponibilidad a la réplica secundaria de confirmación asincrónica durante la actualización gradual. Para impedir la pérdida de datos, cambie el modo de confirmación a confirmación sincrónica y espere a que la réplica secundaria se sincronice antes de conmutar por error al grupo de disponibilidad. Por lo tanto, el proceso de actualización puede ser similar al siguiente:  
  
1.  Actualizar el servidor remoto  
  
2.  Cambiar el modo de confirmación a confirmación sincrónica  
  
3.  Esperar hata que el estado de sincronización sea SINCRONIZADO  
  
4.  Conmutar por error el grupo de disponibilidad al sitio remoto  
  
5.  Actualizar el servidor local (sitio principal)  
  
6.  Conmutar por error el grupo de disponibilidad al sitio principal  
  
7.  Cambiar el modo de confirmación a confirmación asincrónica  
  
 Dado que el modo de confirmación sincrónica no es una opción recomendada para la sincronización de datos en un sitio remoto, las aplicaciones de cliente pueden apreciar un aumento inmediato en la latencia de las bases de datos tras el cambio de configuración. Además, realizar una conmutación por error provocará que todos los mensajes de registro no reconocidos se descarten. La cantidad de mensajes de registro descartados puede ser bastante grande debido a la alta latencia de red entre dos sitios, lo que ocasiona que los clientes experimenten un gran volumen de errores de transacciones. Puede aminorar el impacto en las aplicaciones cliente si hace lo siguiente:  
  
-   Seleccionar cuidadosamente una ventana de mantenimiento durante el tráfico lento de cliente  
  
-   Mientras actualiza SQL Server en el sitio pincipal, cambiar el modo de disponibilidad de nuevo a la confirmación asincrónica y luego revertir al modo sincrónico cuando esté listo para conmutar por error al sitio principal de nuevo  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>Grupo de disponibilidad con nodos de instancia del clúster de conmutación por error  
 Si un grupo de disponibilidad contiene nodos de instancia de clúster de conmutación por error (FCI), debe actualizar los nodos inactivos antes de actualizar los nodos activos. La ilustración siguiente muestra un escenario de grupos de disponibilidad común con FCI para la confirmación asincrónica y una alta disponibilidad local entre los FCI pra la recuperación de desastres remota y la secuencia de actualización.  
  
 ![Actualización de un grupo de disponibilidad con FCI](../../media/agupgrade-ag-fci-dr.gif "Actualización de un grupo de disponibilidad con FCI")  
  
1.  Actualizar REMOTE2  
  
2.  Conmutar por error FCI2 a REMOTE2  
  
3.  Actualizar REMOTE1  
  
4.  Actualizar PRIMARY2  
  
5.  Conmutar por error FCI1 a PRIMARY2  
  
6.  Actualizar PRIMARY1  
  
## <a name="upgradeupdate-sql-server-instances-with-multiple-availability-groups"></a>Actualizar las instancias de SQL Server con varios grupos de disponibilidad  
 Si ejecuta varios grupos de disponibilidad con réplicas principales en nodos de servidor independientes (una configuración activa/activa), la ruta de actualización implica más pasos de conmutación por error para presentar una alta disponibilidad en el proceso. Suponga que ejecuta tres grupos de disponibilidad en tres nodos de servidor según se muestra en la tabla siguiente y que todas las réplicas secundarias se ejecutan en el modo de confirmación sincrónica.  
  
|Grupo de disponibilidad|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Principal|||  
|AG2||Principal||  
|AG3|||Principal|  
  
 Puede ser apropiado en su situación realizar una actualización gradual con equilibrio de carga en la secuencia siguiente:  
  
1.  Conmutar por error AG2 a Nodo3 (para liberar Nodo2)  
  
2.  Actualizar Nodo2  
  
3.  Conmutar por error AG1 a Nodo2 (para liberar Nodo1)  
  
4.  Actualizar Nodo1  
  
5.  Conmutar por error AG2 y AG3 a Nodo1 (para liberar Nodo3)  
  
6.  Actualizar Nodo3  
  
7.  No se puede realizar la conmutación por error de AG3 a Nodo3  
  
 Esta secuencia de actualización tiene un tiempo de inactividad promedio de menos de dos conmutaciones por error por cada grupo de disponibilidad. La configuración resultante se muestra en la tabla siguiente.  
  
|Grupo de disponibilidad|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Principal||  
|AG2|Principal|||  
|AG3|||Principal|  
  
 Según su implementación concreta, la ruta de actualización puede variar y el tiempo de inactividad que las aplicaciones cliente experimentan puede variar también.  
  
  
