---
title: Propiedades de memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a88e2c1508ec849437d90b3de7c66705299dafc1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068893"
---
# <a name="memory-properties"></a>Propiedades de memoria
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de memoria de servidor que aparecen en la siguiente tabla. Para obtener información orientativa acerca de estas propiedades, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Los valores comprendidos entre 1 y 100 representan porcentajes de **Memoria física total** o de **Espacio de direcciones virtuales**, lo que sea menor. Los valores superiores a 100 representan límites de memoria en bytes.  
  
 **Se aplica a:** Modo de servidor multidimensional y Tabular, a menos que se indique lo contrario.  
  
## <a name="properties"></a>Propiedades  
 `LowMemoryLimit`  
 Una propiedad numérica de 64 bits con signo, de punto flotante y de doble precisión que define el punto en el que el servidor tiene poca memoria, expresada como porcentaje de la memoria física total. Cuando se alcanza este límite, la instancia comenzará lentamente a limpiar cachés de la memoria cerrando las sesiones expiradas y descargando los cálculos no utilizados. El servidor no liberará memoria por debajo de este límite. El valor predeterminado es 65, lo que indica que el límite de memoria baja es el 65% de la memoria física o del espacio de direcciones virtuales, lo que sea menor.  
  
 `TotalMemoryLimit`  
 Define un umbral que, cuando se alcanza, hace que el servidor desasigne memoria de forma más enérgica. El valor predeterminado es el 80% de la memoria física o el espacio de direcciones virtuales, lo que sea menor.  
  
 Tenga en cuenta que `TotalMemoryLimit` siempre debe ser menor que `HardMemoryLimit`  
  
 `HardMemoryLimit`  
 Especifica un umbral de memoria a partir del cual la instancia finaliza enérgicamente las sesiones de usuario activas para reducir el uso de memoria. Todas las sesiones finalizadas recibirán un error indicando que la cancelación se ha debido a la presión de memoria. El valor predeterminado, cero (0), significa que `HardMemoryLimit` se establecerá en un valor intermedio comprendido entre `TotalMemoryLimit` y la memoria física total del sistema; si la memoria física del sistema es mayor que el espacio de direcciones virtuales del proceso, se usará dicho espacio para calcular `HardMemoryLimit`.  
  
 `VirtualMemoryLimit`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `VertiPaqPagingPolicy`  
 Especifica el comportamiento de la paginación en caso de que el servidor se quede sin apenas memoria. Los valores válidos son los siguientes:  
  
 Cero (**0**) deshabilita la paginación. Si la memoria es insuficiente, el procesamiento genera un error de memoria insuficiente. Si ha deshabilitado la paginación, debe otorgar privilegios de Windows a la cuenta de servicio. Para obtener instrucciones, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md).  
  
 **1** es el valor predeterminado. Esta propiedad habilita la paginación en disco mediante el archivo de paginación del sistema operativo (pagefile.sys).  
  
 Cuando `VertiPaqPagingPolicy` se establece en 1, es menos probable que se produzcan errores en el procesamiento debido a restricciones de memoria, ya que el servidor intentará paginar en el disco utilizando el método especificado. Establecer la propiedad `VertiPaqPagingPolicy` no garantiza que no se producirán errores de memoria. Pueden seguir produciéndose errores de memoria insuficiente en las siguientes condiciones:  
  
-   No hay suficiente memoria para todos los diccionarios. Durante el procesamiento, Analysis Services bloquea los diccionarios de cada columna en memoria, y todos juntos no pueden superar el valor especificado en `VertiPaqMemoryLimit`.  
  
-   No hay espacio suficiente en las direcciones virtuales para alojar el proceso.  
  
 Para resolver problemas persistentes de memoria insuficiente, puede intentar rediseñar el modelo a fin de reducir la cantidad de datos que necesita procesar o agregar más memoria física al equipo.  
  
 Se aplica solo al modo de servidor tabular.  
  
 `VertiPaqMemoryLimit`  
 Si se permite la paginación en el disco, esta propiedad especifica el nivel de consumo de memoria (como porcentaje de la memoria total) en el que comienza la paginación. El valor predeterminado es 60. Si el consumo de memoria es inferior al 60 por ciento, el servidor no paginará en el disco.  
  
 Esta propiedad depende de `VertiPaqPagingPolicyProperty`, que se debe establecer en 1 para que se produzca la paginación.  
  
 Se aplica solo al modo de servidor tabular.  
  
 `HighMemoryPrice`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryHeapType`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Se aplica solo al modo de servidor multidimensional.  
  
 `HeapTypeForObjects`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Se aplica solo al modo de servidor multidimensional.  
  
 `DefaultPagesCountToReuse`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `HandleIA64AlignmentFaults`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MidMemoryPrice`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MinimumAllocatedMemory`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PreAllocate`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `SessionMemoryLimit`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `WaitCountIfHighMemory`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades del servidor en Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
