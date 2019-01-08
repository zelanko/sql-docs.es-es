---
title: Propiedades de memoria de Analysis Services | Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 763c085e9a4dbc6ecb459ffcd17f5185531b98fb
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072002"
---
# <a name="memory-properties"></a>Propiedades de memoria
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services asigna previamente una pequeña cantidad de memoria durante el inicio para que las peticiones se puedan administrar inmediatamente. Se asigna memoria adicional a medida que aumentan las cargas de trabajo de procesamiento y consultas. 
  
  Al especificar valores de configuración, puede controlar los umbrales en los que se liberará la memoria. Por ejemplo, el valor **HardMemoryLimit** especifica una condición de memoria insuficiente autoimpuesta (de forma predeterminada, este umbral no está habilitado), donde las nuevas peticiones se rechazan de forma absoluta hasta que haya disponibles más recursos.

Para obtener más información acerca de la memoria máxima usada por instancia de SQL Server Analysis Services mediante la edición, vea [ediciones y características admitidas de SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits).
  
 Las siguientes opciones se aplican a servidores tabulares y multidimensionales, a menos que se indique lo contrario.  
 
## <a name="default-memory-configuration"></a>Configuración de memoria predeterminada

En la configuración predeterminada, cada instancia de Analysis Services asigna una pequeña cantidad de RAM (40 MB a 50 MB) al inicio, incluso si la instancia está inactiva. 

Recuerde que los valores de configuración son por instancia. Si ejecuta varias instancias de Analysis Services en el mismo hardware, como una instancia tabular y una multidimensional, cada instancia asignará su propia memoria por separado del resto de las instancias.

En la tabla siguiente se describe brevemente la configuración de memoria más usada (encontrará más información en la sección de referencia). Esta configuración solo si Analysis Services compite por la memoria con otras aplicaciones en el mismo servidor:

Parámetro | Descripción
--------|------------
LowMemoryLimit | Para instancias multidimensionales, un umbral inferior en el que el servidor empieza a liberar memoria asignada a objetos de uso poco frecuente.
VertiPaqMemoryLimit | Para instancias tabulares, un umbral inferior en el que el servidor empieza a liberar memoria asignada a objetos de uso poco frecuente.
TotalMemoryLimit | Un umbral superior en el que Analysis Services empieza a liberar memoria con mayor intensidad para liberar espacio para las peticiones en ejecución, así como para nuevas solicitudes de prioridad alta. 
HardMemoryLimit | Otro umbral en el que Analysis Services empieza a rechazar las peticiones de forma absoluta debido a la presión de memoria. 
 
## <a name="property-reference"></a>Referencia de propiedades

Las propiedades siguientes son válidas para los modos tabular y multidimensional, excepto si se especifica lo contrario.

 Los valores comprendidos entre 1 y 100 representan porcentajes de **Memoria física total** o de **Espacio de direcciones virtuales**, lo que sea menor. Los valores superiores a 100 representan límites de memoria en bytes.
  
 **LowMemoryLimit**  
 Una propiedad con signo 64-bit precisión doble punto flotante número que define el primer umbral en el que Analysis Services empieza a liberar memoria para objetos de prioridad baja, como una memoria caché usado con poca frecuencia. Después de asignar la memoria, el servidor no liberará memoria por debajo de este límite. El valor predeterminado es 65, lo que indica que el límite de memoria baja es el 65% de la memoria física o del espacio de direcciones virtuales, lo que sea menor.  
  
 **TotalMemoryLimit**  
 Define un umbral que, cuando se alcanza, hace que el servidor cancele la asignación de memoria para liberar espacio para otras peticiones. Cuando se alcanza este límite, la instancia comenzará lentamente a limpiar cachés de la memoria cerrando las sesiones expiradas y descargando los cálculos no utilizados. El valor predeterminado es el 80% de la memoria física o el espacio de direcciones virtuales, lo que sea menor. **Valor de TotalMemoryLimit** siempre debe ser menor que **HardMemoryLimit**  
  
 **HardMemoryLimit**  
 Especifica un umbral de memoria a partir del cual la instancia finaliza enérgicamente las sesiones de usuario activas para reducir el uso de memoria. Todas las sesiones finalizadas recibirán un error acerca de la presión de memoria que la cancele. El valor predeterminado, cero (0), significa que **HardMemoryLimit** se establecerá en un valor intermedio comprendido entre **TotalMemoryLimit** y la memoria física total del sistema. Si la memoria física del sistema es mayor que el espacio de direcciones virtuales del proceso, se usará en su lugar el espacio de direcciones virtuales para calcular **HardMemoryLimit**.  

**QueryMemoryLimit**   
Solo Azure Analysis Services. Una propiedad avanzada para controlar cuánta memoria puede usarse por los resultados temporales durante una consulta. Solo se aplica a las medidas DAX y consultas. Consultas MDX en los servidores en modo Multidimensional no usan este límite. No tiene en cuenta para las asignaciones de memoria general usadas por la consulta. Especificada en porcentaje. El valor predeterminado de 0 significa que límite no se especifica.

 **VirtualMemoryLimit**  
  Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **VertiPaqPagingPolicy**  
  Solo para instancias tabulares, especifica el comportamiento de paginación en caso de que el servidor no tenga memoria suficiente. Los valores válidos son los siguientes:  
  
Parámetro  |Descripción  
---------|---------
**0**     |  (valor predeterminado para Azure Analysis Services) Deshabilita la paginación. Si la memoria es insuficiente, el procesamiento genera un error de memoria insuficiente. Si ha deshabilitado la paginación, debe otorgar privilegios de Windows a la cuenta de servicio. Para obtener instrucciones, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md). 
**1**     |  (valor predeterminado de SQL Server Analysis Services) Esta propiedad habilita la paginación en disco mediante el archivo de paginación del sistema operativo (pagefile.sys).   
  
Cuando se establece en 1, es menos probable que se produzcan errores de procesamiento debido a restricciones de memoria, ya que el servidor intentará paginar en el disco con el método que ha especificado. Establecer la propiedad **VertiPaqPagingPolicy** no garantiza que no se producirán errores de memoria. Pueden seguir produciéndose errores de memoria insuficiente en las siguientes condiciones:  
  
-   No hay suficiente memoria para todos los diccionarios. Durante el procesamiento, el servidor bloquea los diccionarios de cada columna en la memoria y todos juntos no pueden superar el valor especificado para **VertiPaqMemoryLimit**.  
  
-   No hay espacio suficiente en las direcciones virtuales para alojar el proceso.  
  
 Para resolver problemas persistentes de memoria insuficiente, puede intentar rediseñar el modelo a fin de reducir la cantidad de datos que necesita procesar o agregar más memoria física al equipo.  
  
 **VertiPaqMemoryLimit**  
 Solo para instancias tabulares, si se permite la paginación en el disco, esta propiedad especifica el nivel de consumo de memoria (como un porcentaje del total de memoria) en que se inicia la paginación. El valor predeterminado es 60. Si el consumo de memoria es inferior al 60 por ciento, el servidor no paginará en el disco. Esta propiedad depende de **VertiPaqPagingPolicyProperty**, que se debe establecer en 1 para que se produzca la paginación.  
  
 **HighMemoryPrice**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryHeapType**  
  Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los valores válidos en SQL Server 2016 SP1 y versiones posteriores de Analysis Services:
  
  Parámetro | Descripción
--------|------------
**-1** | (Valor predeterminado) automático. El motor decidirá cuál valor usar.
**1** | Montón de Analysis Services.
**2** | LFH de Windows.
**5** | Asignador híbrido. Este asignador usará LFH de Windows para \<= las asignaciones de 16 KB y montón de AS para > las asignaciones de 16 KB. 
**6** | Asignador de Intel TBB. Disponible en SQL Server 2016 SP1 y versiones posteriores de Analysis Services.
  
  
 **HeapTypeForObjects**  
  Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los valores válidos son los siguientes:
  
   Parámetro | Descripción
--------|------------
**-1** | (Valor predeterminado) automático. El motor decidirá cuál valor usar.
**0** | Montón de LFH de Windows.
**1** | Asignador de ranuras de Analysis Services.
**3** | Cada objeto tiene su propio montón de Analysis Services.

 
 **DefaultPagesCountToReuse**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **HandleIA64AlignmentFaults**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MidMemoryPrice**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinimumAllocatedMemory**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PreAllocate**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SessionMemoryLimit**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **WaitCountIfHighMemory**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
