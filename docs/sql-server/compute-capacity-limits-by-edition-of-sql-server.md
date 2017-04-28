---
title: "Límites de la capacidad de cálculo de cada edición de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
caps.latest.revision: 60
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f32d9ca838e004676a3cccffbe62bbbc0e46a3f
ms.lasthandoff: 04/11/2017

---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>Compute Capacity Limits by Edition of SQL Server
  En este tema se describen los límites de la capacidad de cálculo para diferentes ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y sus diferencias en entornos físicos y virtualizados con los procesadores hyperthreaded.  
  
 ![Asignaciones para calcular los límites de capacidad](../sql-server/media/compute-capacity-limits.gif "Asignaciones para calcular los límites de capacidad")  
  
 En la tabla siguiente se describen las notaciones que se usan en el diagrama anterior:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0..1|Cero o uno|  
|1|Exactamente uno|  
|1..*|Uno o más|  
|0..*|Cero o más|  
|1..2|Uno o dos|  
  
> [!IMPORTANT]  
>  Información ampliada:  
>   
>  1.  Una máquina virtual se asigna a uno o varios procesadores virtuales.  
> 2.  Uno o más procesadores virtuales se asignan exactamente a una máquina virtual.  
> 3.  Cero o un procesador virtual se asigna a cero o más procesadores lógicos. Cuando el procesador virtual para la asignación lógica del procesador es:  
>   
>      -   Uno a cero, representa un procesador lógico desenlazado no utilizado por los sistemas operativos invitados.  
>     -   Uno a muchos representa un compromiso excesivo.  
>     -   Cero a muchos, representa la ausencia de máquina virtual en el sistema host, por lo que ninguna máquina virtual usa los procesadores lógicos.  
> 4.  Un socket se asigna a cero o más núcleos. Cuando el socket para la asignación de núcleo es:  
>   
>      -   Uno a cero, representa un socket vacío (sin chip instalado).  
>     -   Uno a uno, representa un chip de un solo núcleo instalado en el socket (muy excepcional actualmente).  
>     -   Uno a muchos representa una configuración de varios núcleos instalada en el socket (los valores típicos son 2,4,8).  
> 5.  Un núcleo se asigna a uno o dos procesadores lógicos. Cuando el núcleo para la asignación lógica del procesador es:  
>   
>      -   Uno a uno, el hyperthreading está desactivado.  
>     -   Uno a dos, el hyperthreading está activado.  
  
 Las definiciones siguientes se aplican a los términos usados en este tema:  
  
-   Un subproceso o procesador lógico es un motor de proceso lógico desde la perspectiva de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el sistema operativo, una aplicación o un controlador.  
  
-   Una núcleo es una unidad de procesador, que puede estar formada por uno o varios procesadores lógicos.  
  
-   Un procesador físico puede estar formado por uno o varios núcleos. Un procesador físico es igual que un paquete de procesadores, o socket.  
  
 Los sistemas con más de un procesador físico o con procesadores físicos que tienen varios núcleos y/o hyperthreads permiten al sistema operativo ejecutar varias tareas simultáneamente. Cada subproceso de ejecución aparece como procesador lógico. Por ejemplo, si su equipo tiene dos procesadores de cuatro núcleos con el hyperthreading habilitado y dos subprocesos por núcleo, tiene 16 procesadores lógicos: 2 procesadores x 4 núcleos por procesador x 2 subprocesos por núcleo. Cabe mencionar que:  
  
-   La capacidad de cálculo de un procesador lógico de un solo subproceso de un núcleo hyperthreaded es menor que la capacidad de cálculo de un procesador lógico del mismo núcleo con el hyperthreading deshabilitado.  
  
-   Pero la capacidad de cálculo de los 2 procesadores lógicos del núcleo hyperthreaded es mayor que la capacidad de cálculo del mismo núcleo con el hyperthreading deshabilitado.  
  
 Cada edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene dos límites de capacidad de cálculo:  
  
1.  Un número máximo de sockets (igual que el procesador físico o socket o paquete de procesadores).  
  
2.  Un número máximo de núcleos de los que informó el sistema operativo.  
  
 Estos límites se aplican a una sola instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Representan la capacidad máxima de cálculo que una sola instancia usará. No restringen el servidor en el que se puede implementar la instancia. De hecho, implementar varias instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el mismo servidor físico es una manera eficaz de usar la capacidad de proceso de un servidor físico con más sockets y/o núcleos que los límites de capacidad siguientes.  
  
 En la siguiente tabla se especifican los límites de la capacidad de cálculo para una sola instancia de cada edición de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]:  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Edición|Capacidad máxima de cálculo que usa una sola instancia ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|Capacidad máxima de cálculo que usa una sola instancia (AS, RS)|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition: licencia basada en núcleo*|Sistema operativo máximo|Sistema operativo máximo|  
|Desarrollador|Sistema operativo máximo|Sistema operativo máximo|  
|Standard|Limitada a menos de 4 sockets o 24 núcleos|Limitada a menos de 4 sockets o 24 núcleos|  
|Express|Limitada a menos de 1 socket o 4 núcleos|Limitada a menos de 1 socket o 4 núcleos|  
 *La licencia basada en Enterprise Edition con licencia de servidor y acceso de cliente (CAL) (no disponible para nuevos contratos) está limitada a un máximo de 20 núcleos por instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . No hay ningún límite en el modelo de licencias de servidor basado en núcleos.  
  
 En un entorno virtualizado, el límite de la capacidad de cálculo se basa en el número de procesadores lógicos, no en el de núcleos, porque la arquitectura de procesador no está visible para las aplicaciones invitadas.  Por ejemplo, un servidor con cuatro sockets poblados con procesadores de cuatro núcleos y la capacidad de habilitar dos hyperthreads por núcleo contiene 32 procesadores lógicos el hyperthreading habilitado, pero solo 16 procesadores lógicos con el hyperthreading deshabilitado. Los procesadores lógicos se pueden asignar a máquinas virtuales en el servidor con la carga de cálculo de las máquinas virtuales del procesador lógico asignada a un subproceso de ejecución en el procesador físico del servidor host.  
  
 Puede que desee deshabilitar el hyperthreading cuando el rendimiento de cada procesador virtual es importante. El hyperthreading se puede habilitar o deshabilitar mediante la configuración del BIOS del procesador durante la instalación del BIOS, pero normalmente es una operación de ámbito de servidor que afectará a todas las cargas de trabajo que se ejecutan en el servidor. Esto puede sugerir que se deben separar las cargas de trabajo que se ejecutarán en entornos virtualizados de aquellas que se beneficiarían de aumentar el rendimiento de hyperthreading en un entorno físico del sistema operativo.  
  
## <a name="see-also"></a>Vea también  
 [Ediciones y componentes de SQL Server 2016](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Especificaciones de capacidad máxima para SQL Server](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [Quick-Start Installation of SQL Server 2016 (Instalación de SQL Server 2016)](http://msdn.microsoft.com/library/672afac9-364d-4946-ad5d-8a2d89cf8d81)  
  
  


