---
title: Contadores de rendimiento (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7d4e13542e8361fb9f4bf4fb05509ebe01669ad
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365797"
---
# <a name="performance-counters-ssas"></a>Contadores de rendimiento (SSAS)
  Mediante el Monitor de rendimiento, puede supervisar el rendimiento de una instancia de Microsoft SQL Server Analysis Services (SSAS) mediante contadores de rendimiento.  
  
 El Monitor de rendimiento es un complemento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Control (MMC) que hace un seguimiento del uso de los recursos. Para iniciar este complemento MMC, escriba **PerfMon** en el símbolo del sistema, o bien, en el Panel de control, haga clic en **Herramientas administrativas**y, después, en **Monitor de rendimiento**. El Monitor de rendimiento permite seguir la actividad y el rendimiento de los servidores y los procesos mediante objetos y contadores predefinidos, y supervisar los eventos mediante contadores definidos por el usuario. El Monitor de rendimiento recopila recuentos en lugar de datos sobre los eventos, como, por ejemplo, uso de la memoria, cantidad de transacciones activas o actividad de la CPU. También puede establecer umbrales en contadores específicos para generar alertas que notifiquen a los operadores.  
  
 El Monitor de rendimiento permite supervisar el servidor remoto y las instancias locales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Usar el Monitor de rendimiento](https://technet.microsoft.com/library/cc749115.aspx).  
  
 Para ver la descripción de cualquier contador que se pueda usar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], en el Monitor de rendimiento, abra el cuadro de diálogo **Agregar contadores** , seleccione un objeto de rendimiento y haga clic en **Mostrar descripción**. Los contadores más importantes son el uso de la CPU, el uso de la memoria y la velocidad de E/S del disco. Se recomienda empezar con estos contadores importantes, y pasar a los contadores más detallados cuando tenga una idea mejor de lo que se puede mejorar mediante la supervisión. Para obtener más información sobre qué contadores incluir, vea [Guía de operaciones de SQL Server 2008 R2](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Los contadores están agrupados para que pueda encontrar más fácilmente los contadores relacionados.  
  
## <a name="counters-by-groups"></a>Contadores por grupos  
  
|Agrupar|Descripción|  
|-----------|-----------------|  
|[Caché](#bkmk_Cache)|Estadísticas relacionadas con la memoria caché de agregaciones de Analysis Services.|  
|[Conexión](#bkmk_Connection)|Estadísticas relacionadas con las conexiones de Microsoft Analysis Services.|  
|[Predicción de minería de datos](#bkmk_DataMiningPrediction)|Estadísticas relacionadas con el procesamiento de los modelos de minería de datos.|  
|[Procesamiento del modelo de minería de datos](#bkmk_DataMiningModelProcessing)|Estadísticas relacionadas con la creación de predicciones a partir de los modelos de minería de datos.|  
|[Bloqueos](#bkmk_Locks)|Estadísticas relacionadas con los bloqueos internos del servidor de Microsoft Analysis Services.|  
|[MDX](#bkmk_MDX)|Estadísticas relacionadas con los cálculos MDX de Microsoft Analysis Services.|  
|[Memoria](#bkmk_Memory)|Estadísticas relacionadas con la memoria interna del servidor de Microsoft Analysis Services.|  
|[Almacenamiento en caché automático](#bkmk_ProactiveCaching)|Estadísticas relacionadas con el almacenamiento en caché automático de Microsoft Analysis Services.|  
|[Procesamiento de agregaciones](#bkmk_ProcAggregations)|Estadísticas relacionadas con el procesamiento de agregaciones en archivos de datos MOLAP.|  
|[Procesamiento de índices](#bkmk_ProcIndexes)|Estadísticas relacionadas con el procesamiento de índices para los archivos de datos MOLAP.|  
|[Procesamiento](#bkmk_Processing)|Estadísticas relacionadas con el procesamiento de datos.|  
|[Consulta del motor de almacenamiento](#bkmk_StorageEngineQuery)|Estadísticas relacionadas con las consultas del motor de almacenamiento de Microsoft Analysis Services.|  
|[Subprocesos](#bkmk_Threads)|Estadísticas relacionadas con los subprocesos de Microsoft Analysis Services.|  
  
###  <a name="bkmk_Cache"></a> Caché  
 Estadísticas relacionadas con la caché de agregaciones de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|KB actuales|Memoria actual usada por la caché de agregaciones, en KB.|  
|KB agregados/s|Velocidad de memoria agregada a la caché, KB/s.|  
|Entradas actuales|Número actual de entradas de caché.|  
|Inserciones/s|Velocidad de inserciones en la caché.  El seguimiento de la velocidad se realiza por partición por cubo por base de datos.|  
|Expulsiones/s|Velocidad de expulsiones de la caché.  Es por partición por cubo por base de datos.  Normalmente, las expulsiones son debidas al limpiador de fondo.|  
|Total de inserciones|Inserciones en la caché.  El seguimiento de la velocidad se realiza por partición por cubo por base de datos.|  
|Total de expulsiones|Expulsiones de la caché.  El seguimiento de las expulsiones se realiza por partición por cubo por base de datos.  Normalmente, las expulsiones son debidas al limpiador de fondo.|  
|Aciertos directos/s|Velocidad de aciertos directos de caché. Un acierto de caché indica que las consultas se respondieron a partir de una entrada de caché existente.|  
|Errores/s|Velocidad de errores de caché.|  
|Búsquedas/s|Velocidad de búsquedas de caché.|  
|Total de aciertos directos|Recuento total de aciertos directos de caché.  Un acierto directo de caché indica que las consultas se respondieron a partir de entradas de caché existentes.|  
|Total de errores|Recuento total de errores de caché.|  
|Total de búsquedas|Número total de búsquedas en la caché.|  
|Relación de aciertos directos|Relación de aciertos directos de caché en búsquedas de caché, durante el período de obtención de valores de contador.|  
|Total de aciertos de caché del elemento de iterador filtrados|Número total de aciertos de caché que devolvió un elemento de iterador indexado en relación con los resultados filtrados.|  
|Total de errores de caché del elemento de iterador filtrados|Número total de aciertos de caché que no pudieron generar un iterador indizado en relación con los resultados filtrados y tuvieron que generar otra caché con dichos resultados.|  
  
###  <a name="bkmk_Connection"></a> Conexión  
 Estadísticas relacionadas con las conexiones de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Conexiones actuales|Número actual de conexiones de cliente establecidas.|  
|Solicitudes/s|Velocidad de solicitudes de conexión.  Se trata de llegadas.|  
|Total de solicitudes|Total de solicitudes de conexión.  Se trata de llegadas.|  
|Conexiones realizadas correctamente/s|Velocidad de finalizaciones de conexión realizadas correctamente.|  
|Total de conexiones realizadas correctamente|Total de conexiones realizadas correctamente.|  
|Errores/s|Velocidad de errores de conexión.|  
|Total de errores|Total de intentos de conexión con error.|  
|Sesiones de usuarios actuales|Número actual de sesiones de usuarios establecidas.|  
  
###  <a name="bkmk_DataMiningModelProcessing"></a> Procesamiento del modelo de minería de datos  
 Estadísticas relacionadas con el procesamiento del modelo de minería de datos de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Casos/s|Velocidad a la que se procesan los casos.|  
|Procesamiento actual de modelos|Número actual de modelos en proceso.|  
  
###  <a name="bkmk_DataMiningPrediction"></a> Predicción de minería de datos  
 Estadísticas relacionadas con la predicción de minería de datos de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Consultas de minería simultáneas|Número actual de consultas de minería de datos en las que se está trabajando activamente.|  
|Predicciones/s|Número de predicciones generadas en las consultas de minería de datos|  
|Filas/s|Número de filas procesadas durante una consulta de predicción de minería de datos.|  
|Consultas/s|Número de consultas de minería de datos procesadas.|  
|Total de consultas|Total de consultas de minería de datos recibidas por el servidor.|  
|Filas de totales|Total de filas devueltas por consultas de minería de datos.|  
|Total de predicciones|Total de consultas de predicciones de minería de datos recibidas por el servidor.|  
  
###  <a name="bkmk_Locks"></a> Bloqueos  
 Estadísticas relacionadas con los bloqueos internos del servidor de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Esperas de bloqueos temporales|Número actual de subprocesos que esperan un bloqueo temporal.  Se trata de solicitudes de bloqueos temporales que no se han podido satisfacer de inmediato y que están en un estado de espera.|  
|Esperas de bloqueos temporales/s|Velocidad de solicitudes de bloqueos temporales que no se han podido satisfacer de inmediato y que han tenido que esperar antes de ser concedidas.|  
|Bloqueos actuales|Número actual de objetos bloqueados.|  
|Esperas de bloqueo actuales|Número actual de clientes que esperan un bloqueo.|  
|Solicitudes de bloqueo/s|Número de solicitudes de bloqueo por segundo.|  
|Concesiones de bloqueo/s|Número de concesiones de bloqueo por segundo.|  
|Esperas de bloqueo/s|Número de esperas de bloqueo por segundo.  Se trata de solicitudes de bloqueo que no han podido obtener el bloqueo de inmediato y que se han puesto en un estado de espera.|  
|Denegaciones de bloqueo/s|Velocidad de denegaciones de bloqueo.|  
|Solicitudes de desbloqueo/s|Número de solicitudes de desbloqueo por segundo.|  
|Total de interbloqueos detectados|Número total de interbloqueos detectados.|  
  
###  <a name="bkmk_MDX"></a> MDX  
 Estadísticas relacionadas con los cálculos MDX de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Número de cubiertas de cálculos|Número total de nodos de evaluación generados por planes de ejecución MDX, incluidos los activos y los de la caché.|  
|Número actual de nodos de evaluación|Número (aproximado) actual de nodos de evaluación generados por planes de ejecución MDX, incluidos los activos y los almacenados en caché.|  
|Número de nodos de evaluación del motor de almacenamiento|Número total de nodos de evaluación del motor de almacenamiento generados por planes de ejecución MDX.|  
|Número de nodos de evaluación celda por celda|Número total de nodos de evaluación celda por celda generados por planes de ejecución MDX.|  
|Número de nodos de evaluación de modo masivo|Número total de nodos de evaluación de modo masivo generados por planes de ejecución MDX.|  
|Número de nodos de evaluación que incluían una sola celda|Número total de nodos de evaluación generados por planes de ejecución MDX que incluían una sola celda.|  
|Número de nodos de evaluación con cálculos con la misma granularidad|Número total de nodos de evaluación generados por planes de ejecución MDX para los cuales los cálculos tenían la misma granularidad que el nodo de evaluación.|  
|Número actual de nodos de evaluación almacenados en caché|Número (aproximado) actual de nodos de evaluación almacenados en caché generados por planes de ejecución MDX.|  
|Número de nodos de evaluación del motor de almacenamiento almacenados en caché|Número total de nodos de evaluación del motor de almacenamiento almacenados en caché generados por planes de ejecución MDX.|  
|Número de nodos de evaluación de modo masivo almacenados en caché|Número total de nodos de evaluación de modo masivo generados por planes de ejecución MDX almacenados en caché.|  
|Número de nodos de evaluación de otro tipo almacenados en caché|Número total de nodos de evaluación de modo masivo generados por planes de ejecución MDX almacenados en caché que no son del motor de almacenamiento ni de modo masivo.|  
|Número de expulsiones de nodos de evaluación|Número total de expulsiones de la caché de nodos de evaluación como consecuencia de colisiones.|  
|Número de aciertos de índice de hash de nodos de evaluación en la caché|Número total de aciertos de nodos de evaluación de la caché correctos con el índice de hash.|  
|Número de aciertos celda por celda de nodos de evaluación de la caché|Número total de aciertos celda por celda de nodos de evaluación de la caché.|  
|Número de errores celda por celda de nodos de evaluación de la caché|Número total de errores celda por celda de nodos de evaluación de la caché.|  
|Número de aciertos de subcubo de nodos de evaluación de la caché|Número total de aciertos de subcubo de nodos de evaluación de la caché.|  
|Número de errores de subcubo de nodos de evaluación de la caché|Número total de errores de subcubo de nodos de evaluación de la caché.|  
|Total de subcubos sónar|Número total de subcubos generado por el optimizador de consultas.|  
|Total de celdas calculadas|Número total de propiedades de celda calculadas.|  
|Total de cálculos repetidos|Número total de celdas recalculadas debido a errores.|  
|Total de inserciones en caché sin formato|Número total de valores de celda insertados en la caché de cálculo sin formato.|  
|Total de caché de cálculo registrada|Número total de cachés de cálculo registradas.|  
|Total de NON EMPTY|Número total de veces que se utiliza un algoritmo NON EMPTY.|  
|Total de NON EMPTY no optimizados|Número total de veces que se utiliza un algoritmo no optimizado NON EMPTY.|  
|Total de NON EMPTY para miembros calculados|Número total de veces que un algoritmo NON EMPTY entró en bucle en miembros calculados.|  
|Total de Autoexist|Número total de veces que se realizó Autoexist.|  
|Total de EXISTING|Número total de veces que se realizó una operación de conjuntos EXISTING.|  
  
###  <a name="bkmk_Memory"></a> Memoria  
 Estadísticas relacionadas con la memoria interna del servidor de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|64 KB asignados de bloque paginado|Memoria prestada del sistema, en KB.  Esta memoria se cede a otras partes del servidor.|  
|64 KB en lista de direcciones de bloque paginado|Memoria actual en lista de direcciones de 64 KB, en KB.  (Páginas de memoria listas para utilizarlas).|  
|8 KB asignados de bloque paginado|Memoria prestada de grupo de páginas de 64 KB, en KB.  Esta memoria se cede a otras partes del servidor.|  
|8 KB en lista de direcciones de bloque paginado|Memoria actual en lista de direcciones de 8 KB, en KB.  (Páginas de memoria listas para utilizarlas).|  
|1 KB asignado de bloque paginado|Memoria prestada de grupo de páginas de 64 KB, en KB.  Esta memoria se cede a otras partes del servidor.|  
|1 KB en lista de direcciones de bloque paginado|Memoria actual en lista de direcciones de 8 KB, en KB.  (Páginas de memoria listas para utilizarlas).|  
|Precio actual de limpiador|Precio actual de memoria, $/byte/tiempo, normalizado a 1000.|  
|Balance de limpiador/s|Velocidad de operaciones de balance+reducción.|  
|KB de memoria de limpiador reducida/s|Velocidad de reducción, en KB/s.|  
|KB reducibles de memoria de limpiador|Cantidad de memoria, en KB, que purgará el limpiador en segundo plano.|  
|KB no reducibles de memoria de limpiador|Cantidad de memoria, en KB, que no purgará el limpiador en segundo plano.|  
|KB de memoria de limpiador|Cantidad de memoria, en KB, conocida por el limpiador en segundo plano.  (KB reducibles de memoria de limpiador + KB no reducibles de memoria de limpiador).|  
|KB de uso de memoria|Uso de memoria del proceso de servidor tal como se usa para calcular el precio de la memoria del limpiador.  Es igual al contador Proceso\Bytes privados más el tamaño de los datos asignados a la memoria; se omite la memoria que ha asignado el motor analítico en memoria xVelocity (VertiPaq) superior al límite de memoria del motor xVelocity.|  
|KB de límite bajo de memoria|Límite de memoria baja del archivo de configuración.|  
|KB de límite alto de memoria|Límite de memoria alta del archivo de configuración.|  
|KB caché agregación|Memoria actual asignada a caché de agregaciones, en KB.|  
|KB de cuota|Cuota de memoria actual, en KB.  La cuota de memoria también se denomina concesión de memoria o reserva de memoria.|  
|Cuota bloqueada|Número actual de solicitudes de cuota que están bloqueadas hasta que se liberen otras cuotas de memoria.|  
|KB de almacén de archivos|Memoria actual asignada a almacén de archivos (caché de archivos), en KB.|  
|Errores de página de almacén de archivos/s|Velocidad de errores de página de almacén de archivos.|  
|Lecturas de almacén de archivos/s|Páginas de almacén de archivos leídas/s|  
|Lecturas de KB de almacén de archivos/s|KB de almacén de archivos leídos/s|  
|Escrituras de almacén de archivos/s|Páginas de almacén de archivos escritas/seg. Las escrituras son asincrónicas.|  
|Escritura de KB de almacén de archivos/s|KB de almacén de archivos escritos/seg. Las escrituras son asincrónicas.|  
|Errores de E/S de almacén de archivos/s|Velocidad de errores de E/S de almacén de archivos.|  
|Errores de E/S de almacén de archivos|Total de errores de E/S de almacén de archivos.|  
|Páginas de reloj de almacén de archivos examinadas/s|Velocidad del limpiador en segundo plano al examinar páginas para posibles expulsiones.|  
|Páginas de reloj de almacén de archivos HaveRef/s|Velocidad del limpiador en segundo plano al examinar páginas que tienen una cuenta de referencias actual (en uso actualmente).|  
|Páginas de reloj de almacén de archivos válidas/s|Velocidad del limpiador en segundo plano al examinar páginas que son candidatas válidas para su expulsión.|  
|KB fijados de memoria de almacén de archivos|KB fijados actuales de memoria de almacén de archivos.|  
|KB de archivo de propiedades de dimensión en memoria|Tamaño actual del archivo de propiedades de dimensión en memoria, en KB.|  
|KB de archivo de propiedades de dimensión en memoria/s|Velocidad de escritura en el archivo de propiedades de dimensión en memoria, en KB.|  
|KB potenciales de archivo de propiedades de dimensión en memoria|Tamaño potencial del archivo de propiedades de dimensión en memoria, en KB.|  
|Archivos de propiedades de dimensión|Número de archivos de propiedades de dimensión.|  
|KB de archivo (hash) de índice de dimensión en memoria|Tamaño del archivo (hash) de índice de dimensión en memoria actual, en KB.|  
|KB de archivo (hash) de índice de dimensión en memoria/s|Velocidad de escritura en el archivo (hash) de índice de dimensión en memoria, en KB.|  
|KB potenciales de archivo (hash) de índice de dimensión en memoria|Tamaño potencial del archivo (hash) de índice de dimensión en memoria, en KB.|  
|Archivos (hash) de índice de dimensión|Número de archivos (hash) de índice de dimensión.|  
|KB de archivo de cadena de dimensión en memoria|Tamaño actual del archivo de cadena de dimensión en memoria, en KB.|  
|KB de archivo de cadena de dimensión en memoria/s|Velocidad de escritura en el archivo de cadena de dimensión en memoria, en KB.|  
|KB potenciales de archivo de cadena de dimensión en memoria|Tamaño potencial del archivo de cadena de dimensión en memoria, en KB.|  
|Archivos de cadena de dimensión|Número de archivos de cadena de dimensión.|  
|KB de archivo de asignación en memoria|Tamaño actual del archivo de asignación en memoria, en KB.|  
|KB de archivo de asignación en memoria/s|Velocidad de escritura en el archivo de asignación en memoria, en KB.|  
|KB potenciales de archivo de asignación en memoria|Tamaño potencial del archivo de asignación en memoria, en KB.|  
|Archivos de asignación|Número de archivos de asignación.|  
|KB de archivo de asignación de agregación en memoria|Tamaño actual del archivo de asignación de agregación en memoria, en KB.|  
|KB de archivo de asignación de agregación en memoria/s|Velocidad de escritura en el archivo de asignación de agregación en memoria, en KB.|  
|KB potenciales de archivo de asignación de agregación en memoria|Tamaño potencial del archivo de asignación de agregación en memoria, en KB.|  
|Archivos de asignación de agregación|Número de archivos de asignación de agregación.|  
|KB de archivo de datos de hechos en memoria|Tamaño del archivo de datos de hechos en memoria actual, en KB.|  
|KB de archivo de datos de hechos en memoria/s|Velocidad de escritura en el archivo de datos de hechos en memoria, en KB.|  
|KB potenciales de archivo de datos de hechos en memoria|Tamaño potencial del archivo de datos de hechos en memoria, en KB.|  
|Archivos de datos de hechos|Número de archivos de datos de hechos.|  
|KB de archivo de cadena de hechos en memoria|Tamaño del archivo de cadena de hechos en memoria actual, en KB.|  
|KB de archivo de cadena de hechos en memoria/s|Velocidad de escritura en el archivo de cadena de hechos en memoria, en KB.|  
|KB potenciales de archivo de cadena de hechos en memoria|Tamaño potencial del archivo de cadena de hechos en memoria, en KB.|  
|Archivos de cadena de hechos|Número de archivos de cadena de hechos.|  
|KB de archivo de agregación de hechos en memoria|Tamaño actual del archivo de agregación de hechos en memoria, en KB.|  
|KB de archivo de agregación de hechos en memoria/s|Velocidad de escritura en el archivo de agregación de hechos en memoria, en KB.|  
|KB potenciales de archivo de agregación de hechos en memoria|Tamaño potencial del archivo de agregación de hechos en memoria, en KB.|  
|Archivos de agregación de hechos|Número de archivos de agregación de hechos.|  
|KB de otro archivo en memoria|Tamaño de otro archivo en memoria actual, en KB.|  
|KB de otro archivo en memoria/s|Velocidad de escritura en otro archivo en memoria, en KB.|  
|KB potenciales de otro archivo en memoria|Tamaño potencial de otro archivo en memoria, en KB.|  
|Otros archivos|Número de otros archivos.|  
|KB empaquetados de VertiPaq|Kilobytes de memoria paginada en uso para datos en memoria.|  
|KB no paginados de VertiPaq|Kilobytes de memoria bloqueada en el conjunto de trabajo para que la use el motor en memoria.|  
|KB asignados en memoria de VertiPaq|Kilobytes de memoria paginable en uso para datos en memoria.|  
|KB de límite físico de memoria|Límite de memoria física del archivo de configuración.|  
|KB de VertiPaq de límite de memoria|Límite en memoria del archivo de configuración.|  
  
###  <a name="bkmk_ProactiveCaching"></a> Almacenamiento en caché automático  
 Estadísticas relacionadas con el almacenamiento en caché automático de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Notificaciones/s|Velocidad de notificaciones de la base de datos relacional.|  
|Cancelaciones de procesamiento/s|Velocidad de cancelaciones de procesamiento producidas por notificaciones.|  
|Inicio de almacenamiento en caché automático/s|Velocidad de inicio de almacenamiento en caché automático.|  
|Finalización de almacenamiento en caché automático/s|Velocidad de finalización de almacenamiento en caché automático.|  
  
###  <a name="bkmk_ProcAggregations"></a> Procesamiento de agregaciones  
 Estadísticas relacionadas con el procesamiento de agregaciones de Microsoft Analysis Services en archivos de datos MOLAP.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Particiones actuales|Número actual de particiones en proceso.|  
|Total de particiones|Número total de particiones procesadas (correcta o incorrectamente).|  
|Filas de tamaño de memoria|Tamaño de agregaciones actuales en la memoria.  Se trata de un recuento estimado.|  
|Bytes de tamaño de memoria|Tamaño de agregaciones actuales en la memoria.  Se trata de un recuento estimado.|  
|Filas combinadas/s|Velocidad de filas combinadas o insertadas en una agregación.|  
|Filas creadas/s|Velocidad de filas de agregación creadas.|  
|Filas de archivo temporal escritas/s|Velocidad de escritura de filas en un archivo temporal.  En los archivos temporales se escribe cuando las agregaciones superan los límites de memoria.|  
|Bytes de archivo temporal escritos/s|Velocidad de escritura de bytes en un archivo temporal.  En los archivos temporales se escribe cuando las agregaciones superan los límites de memoria.|  
  
###  <a name="bkmk_ProcIndexes"></a> Procesamiento de índices  
 Estadísticas relacionadas con el procesamiento de índices de Microsoft Analysis Services para archivos de datos MOLAP.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Particiones actuales|Número actual de particiones en proceso.|  
|Total de particiones|Número total de particiones procesadas (correcta o incorrectamente).|  
|Filas/s|Velocidad de filas de archivos MOLAP utilizadas para crear índices.|  
|Filas de totales|Total de filas de archivos MOLAP utilizadas para crear índices.|  
  
###  <a name="bkmk_Processing"></a> Procesamiento  
 Estadísticas relacionadas con el procesamiento de datos de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Filas leídas/s|Velocidad de filas leídas en todas las bases de datos relacionales.|  
|Total de filas leídas|Recuento de filas leídas en todas las bases de datos relacionales.|  
|Filas convertidas/s|Velocidad de filas convertidas durante el procesamiento.|  
|Total de filas convertidas|Recuento de filas convertidas durante el procesamiento.|  
|Filas escritas/s|Velocidad de filas escritas durante el procesamiento.|  
|Total de filas escritas|Recuento de filas escritas durante el procesamiento.|  
  
###  <a name="bkmk_StorageEngineQuery"></a> Consulta del motor de almacenamiento  
 Estadísticas relacionadas con las consultas del motor de almacenamiento de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Consultas de grupo de medida actuales|Número actual de consultas de grupo de medida en las que se está trabajando activamente.|  
|Consultas de grupo de medida/s|Velocidad de consultas de grupo de medida|  
|Total de consultas de grupo de medida|Número total de consultas al grupo de medida.|  
|Consultas de dimensión actuales|Número actual de consultas de dimensión en las que se está trabajando activamente.|  
|Consultas de dimensión/s|Velocidad de consultas de dimensión|  
|Total de consultas de dimensión.|Número total de consultas de dimensión.|  
|Consultas respondidas/s|Velocidad de consultas respondidas.|  
|Total de consultas respondidas|Número total de consultas respondidas.|  
|Bytes enviados/s|Velocidad de bytes enviados por el servidor a clientes, en respuesta a consultas.|  
|Total de bytes enviados|Total de bytes enviados por el servidor a clientes, en respuesta a consultas.|  
|Filas enviadas/s|Velocidad de filas enviadas por el servidor a clientes.|  
|Total de filas enviadas|Total de filas enviadas por el servidor a clientes.|  
|Consultas directas de caché/s|Velocidad de consultas respondidas directamente desde la caché.|  
|Consultas de caché filtradas/s|Velocidad de consultas respondidas filtrando entradas de caché existentes.|  
|Consultas de archivo/s|Velocidad de consultas respondidas desde archivos.|  
|Total de consultas directas de caché|Número total de consultas derivadas directamente de la caché.  Tenga en cuenta que es por partición.|  
|Total de consultas de caché filtradas|Total de consultas respondidas filtrando entradas de caché existentes.|  
|Total de consultas de archivo|Número total de consultas respondidas desde archivos.|  
|Lecturas de asignación/s|Número de operaciones de lectura lógicas mediante el archivo de asignación.|  
|Bytes de asignación/s|Bytes leídos del archivo de asignación.|  
|Lecturas de datos/s|Número de operaciones de lectura lógicas mediante el archivo de datos.|  
|Bytes de datos/s|Bytes leídos del archivo de datos.|  
|Promedio de tiempo/consulta|Promedio de tiempo por consulta en milisegundos.  Tiempo de respuesta basado en consultas respondidas desde la última medida de contador.|  
|Ciclos de ida y vuelta de red/s|Velocidad de ciclos de ida y vuelta de red.  Incluye toda la comunicación cliente/servidor.|  
|Total de ciclos de ida y vuelta de red|Total de ciclos de ida y vuelta de red.  Incluye toda la comunicación cliente/servidor.|  
|Búsquedas de caché sin formato/s|Frecuencia de búsquedas de caché sin formato.  Incluye la caché sin formato de ámbito de consultas, de sesiones y global.|  
|Aciertos de caché sin formato/s|Frecuencia de aciertos de caché sin formato.  Incluye la caché sin formato de ámbito de consultas, de sesiones y global.|  
|Búsquedas de caché de cálculo/s|Frecuencia de búsquedas de caché de cálculo.  Incluye la caché sin formato de ámbito de consultas, de sesiones y global.|  
|Aciertos de caché de cálculo/s|Frecuencia de aciertos de caché de cálculo.  Incluye la caché sin formato de ámbito de consultas, de sesiones y global.|  
|Búsquedas de caché conservada/s|Frecuencia de búsquedas de caché conservada.  La instrucción CACHE de script MDX crea las memorias caché conservadas.|  
|Aciertos de caché conservada/s|Frecuencia de aciertos de caché conservada.  La instrucción CACHE de script MDX crea las memorias caché conservadas.|  
|Búsquedas de caché de dimensión/s|Frecuencia de búsquedas de caché de dimensión/s.|  
|Aciertos de caché de dimensión/s|Frecuencia de aciertos de caché de dimensión.|  
|Búsquedas de caché de grupo de medida/s|Frecuencia de búsquedas de caché de grupo de medida.|  
|Aciertos de caché de grupo de medida/s|Frecuencia de aciertos de caché de grupo de medida.|  
|Búsquedas de agregación/s|Frecuencia de búsquedas de agregación.|  
|Aciertos de agregación/s|Frecuencia de aciertos de agregación.|  
  
###  <a name="bkmk_Threads"></a> Subprocesos  
 Estadísticas relacionadas con los subprocesos de Microsoft Analysis Services.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|Subprocesos inactivos de análisis corto|Número de subprocesos inactivos en el grupo de subprocesos de análisis corto.|  
|Subprocesos ocupados de análisis corto|Número de subprocesos ocupados en el grupo de subprocesos de análisis corto.|  
|Longitud de cola de trabajos de análisis corto|Número de trabajos en la cola del grupo de subprocesos de análisis corto.|  
|Velocidad de trabajos de análisis corto|Velocidad de los trabajos en el grupo de subprocesos de análisis corto.|  
|Subprocesos inactivos de análisis largo|Número de subprocesos inactivos en el grupo de subprocesos de análisis largo.|  
|Subprocesos ocupados de análisis largo|Número de subprocesos ocupados en el grupo de subprocesos de análisis largo.|  
|Longitud de cola de trabajos de análisis largo|Número de trabajos en la cola del grupo de subprocesos de análisis largo.|  
|Velocidad de trabajos de análisis largo|Velocidad de los trabajos en el grupo de subprocesos de análisis largo.|  
|Subprocesos inactivos de grupo de consultas|Número de subprocesos inactivos en el grupo de subprocesos de consulta.|  
|Subprocesos ocupados de grupo de consultas|Número de subprocesos ocupados en el grupo de subprocesos de consulta.|  
|Longitud de cola de trabajos de grupo de consultas|Número de trabajos en la cola del grupo de subprocesos de consulta.|  
|Velocidad de trabajos de grupo de consultas|Velocidad de los trabajos en el grupo de subprocesos de consulta.|  
|Subprocesos inactivos del grupo de procesamiento que no son de E/S|Número de subprocesos inactivos en el grupo de subprocesos de procesamiento dedicados a trabajos que no son de E/S.|  
|Subprocesos ocupados del grupo de procesamiento que no son de E/S|Número de subprocesos del grupo de subprocesos de procesamiento dedicados a trabajos que no son de E/S.|  
|Longitud de cola de trabajos de grupo de procesamiento|Número de trabajos que no son de E/S en la cola del grupo de subprocesos de procesamiento.|  
|Velocidad de trabajos de grupo de procesamiento|Porcentaje de trabajos que no son de E/S completados en el grupo de subprocesos de procesamiento.|  
|Subprocesos inactivos de trabajos de E/S del grupo de procesamiento|Número de subprocesos inactivos del grupo de subprocesos de procesamiento dedicados a trabajos de E/S.|  
|Subprocesos ocupados de trabajos de E/S del grupo de procesamiento|Número de subprocesos del grupo de subprocesos de procesamiento dedicados a trabajos de E/S.|  
|Longitud de la cola de trabajos de E/S del grupo de procesamiento|Número de trabajos de E/S en la cola del grupo de subprocesos de procesamiento.|  
|Porcentaje de trabajos de E/S completados del grupo de procesamiento|Porcentaje de trabajos de E/S completados en el grupo de subprocesos de procesamiento.|  
  
  
