---
title: Configurar la actualización de datos dedicada o el procesamiento de solo consulta (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5e027605-1086-4941-bb01-f315df8f829b
author: minewiskan
ms.author: owend
ms.openlocfilehash: f67cc581c177f5d07df035927eb979c09061a537
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527301"
---
# <a name="configure-dedicated-data-refresh-or-query-only-processing-powerpivot-for-sharepoint"></a>Configurar la actualización de datos dedicada o el proceso de una sola consulta (PowerPivot para SharePoint)
  En el modo integrado de SharePoint, se puede configurar una instancia del servidor de Analysis Services para admitir un tipo específico de solicitud de procesamiento, como la actualización de datos o el procesamiento de una sola consulta. De forma predeterminada, ambos tipos de solicitudes de carga están habilitados. Puede desactivar cualquiera de los tipos para crear un motor de consulta dedicado o un servidor de actualización de datos.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
> [!NOTE]  
>  En esta versión, no hay ninguna configuración para limitar el uso de la memoria o de la CPU para los trabajos de actualización de datos o las consultas a petición. Una instancia de [!INCLUDE[ssGeminiSrv](../includes/ssgeminisrv-md.md)] utilizará todos los recursos que estén disponibles para ejecutar las consultas y los trabajos de actualización de datos que administra.  
  
 Este tema contiene las siguientes secciones:  
  
 [Configurar un modo de procesamiento](#config)  
  
 [Cambiar el número de trabajos de actualización de datos que se pueden ejecutar en paralelo](#change)  
  
##  <a name="configure-a-processing-mode"></a><a name="config"></a>Configurar un modo de procesamiento  
  
1.  En administración central, en configuración del sistema, haga clic en **administrar servicios en el servidor**.  
  
2.  En la parte superior de la página, en Servidor, haga clic en la flecha abajo y, a continuación, haga clic en **Cambiar el servidor**.  
  
3.  Seleccione el servidor de SharePoint que tenga la instancia de servidor de Analysis Services que desea configurar.  
  
4.  Haga clic en **SQL Server Analysis Services**.  
  
5.  En Uso de instancia del servidor, elija entre lo siguiente:  
  
    1.  Desactive la casilla **Habilitar la carga de bases de datos de solo lectura** para desactivar el procesamiento de consultas a petición que se produce cada vez que un usuario abre un libro que contiene datos PowerPivot.  
  
    2.  Desactive la casilla **Habilitar la carga de bases** de datos para la actualización para desactivar la actualización de datos programada.  
  
    > [!NOTE]  
    >  Al desactivar la actualización de datos, las opciones de actualización de datos no se quitan de los sitios de SharePoint. Los usuarios que posean libros PowerPivot siguen pudiendo crear programaciones para la actualización de datos, pero esta no se producirá en ese servidor.  
  
6.  Opcionalmente, en las operaciones de actualización de datos, puede cambiar el número de trabajos de actualización simultáneos. Se recomienda aumentar el número de trabajos simultáneos si el servidor solo se configura para la actualización de datos, o si hay procesadores adicionales en el servidor. Podría disminuir el número de trabajos simultáneos si desea liberar recursos del sistema para más consultas a petición.  
  
7.  Guarde los cambios. El servidor no validará sus entradas hasta que se produzca un evento de procesamiento. Si escribe un número no válido de trabajos simultáneos, el error se detectará y registrar cuando se procese la solicitud siguiente.  
  
##  <a name="change-the-number-of-data-refresh-jobs-that-can-run-in-parallel"></a><a name="change"></a>Cambiar el número de trabajos de actualización de datos que se pueden ejecutar en paralelo  
 Un trabajo de actualización de datos es una tarea programada que se agrega a una cola de procesamiento que una aplicación de servicio PowerPivot mantiene y supervisa. Un trabajo está compuesto de información de programación para uno o más orígenes de datos en un libro PowerPivot. Para cada programación que se define se crea un trabajo independiente. Si el propietario de un libro define una programación para todos los orígenes de datos, solo se creará un trabajo para toda la operación de actualización de datos. Si el propietario de un libro crea programaciones individuales para orígenes de datos externos, se crearán varios trabajos y se ejecutarán para completar una actualización de datos completa para ese libro.  
  
 Puede aumentar el número de trabajos de actualización de datos que se pueden ejecutar al mismo tiempo si el sistema tiene la capacidad de admitir carga adicional.  
  
|Configuración|Valores válidos|Descripción|  
|-------------|------------------|-----------------|  
|Valor predeterminado|Se calcula en función de la RAM.|El valor predeterminado se basa en la cantidad de memoria disponible dividida entre 4 gigabytes. Una fórmula calcula el valor predeterminado para que la configuración se pueda ajustar en función de las capacidades del sistema.<br /><br /> Nota: el divisor de 4 gigabytes se seleccionó en función del uso de RAM para un gran muestreo de orígenes de datos PowerPivot reales. No se basa en la arquitectura física o lógica de PowerPivot.|  
|Valor máximo|Se calcula en función del número de CPU.|El número máximo de trabajos simultáneos que puede especificar se basa en el número de procesadores del equipo. Por ejemplo, en un equipo de cuatro núcleos y cuatros sockets, el número máximo de trabajos que puede ejecutar de forma simultánea es 16.|  
  
#### <a name="increasing-the-default-value-to-a-higher-value"></a>Aumentar el valor predeterminado a un valor más alto  
 El siguiente gráfico muestra diferentes combinaciones de RAM y CPU, así como el valor predeterminado resultante y los valores máximos que se calculan en función de las características del sistema. Recuerde que el valor predeterminado calculado para el número de trabajos de actualización de datos que se pueden ejecutar simultáneamente se basa en la memoria del sistema, mientras que el valor máximo calculado se basa en las CPU. La última indica si se puede aumentar el número máximo de trabajos simultáneos de actualización de datos.  
  
|RAM real (en gigabytes)|Valor predeterminado calculado|Número de CPU reales|Valor máximo calculado|¿Aumentan los trabajos simultáneos?|  
|---------------------------------|------------------------------|------------------------|------------------------------|-------------------------------|  
|4|1|1|1|No. El valor predeterminado y máximo son los mismos.|  
|4|1|4|4|Sí. Puede aumentar el número de trabajos simultáneos a 2, 3 ó 4.|  
|8|2|4|4|Sí. Puede aumentar el número de trabajos simultáneos a 3 ó 4.|  
|16|4|4|4|No. El valor predeterminado y máximo son los mismos.|  
|32|Si se utilizara la fórmula de cálculo del valor predeterminado, este sería 8. Dado que el valor predeterminado es más alto que el máximo permitido, el valor predeterminado calculado no se utiliza en este caso.|4|4|No. Aunque una RAM grande indicaría un valor predeterminado de ocho trabajos simultáneos, un equipo que solo cuatro procesadores admitirá como máximo cuatro trabajos simultáneos.|  
|32|8|8|8|No.|  
|32|8|16|16|Sí.|  
|64|16|16|16|No.|  
  
 Dado que no hay ninguna manera de conocer de antemano si se pueden ejecutar varios trabajos correctamente al mismo tiempo, solo debería aumentar el número de trabajos simultáneos cuando haya analizado el consumo de memoria a lo largo del tiempo y haya determinado que la memoria del servidor generalmente está infrautilizada.  
  
 Cada trabajo de actualización de datos tendrá características de carga diferentes que dependen del número y tamaño de los orígenes de datos que se están actualizando. Los libros que tienen un único origen de datos con un número menor de filas tienen una carga de procesamiento mucho más ligera que un libro que tiene numerosos orígenes de datos y conjuntos de filas muy grandes.  
  
## <a name="see-also"></a>Consulte también  
 [Actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
