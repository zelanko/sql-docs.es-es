---
title: Change Data Capture (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental loads [SQL Server change data capture]
- change data capture [SQL Server], Integration Services and
ms.assetid: c4aaba1b-73e5-4187-a97b-61c10069cc5a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ccc292cda8b3263c7e1457a52e4426dc9d24460d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263241"
---
# <a name="change-data-capture-ssis"></a>Captura de datos modificados (SSIS)
  En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la captura de datos modificados ofrece una solución efectiva al desafío de realizar eficazmente las cargas incrementales de las tablas de origen a los data mart y a los almacenamientos de datos.  
  
## <a name="what-is-change-data-capture"></a>¿Qué es la captura de datos modificados?  
 Las tablas de origen cambian con el tiempo. Un data mart o un almacenamiento de datos basado en dichas tablas necesita reflejar estos cambios. Sin embargo, un proceso que copie periódicamente una instantánea del origen completo consume demasiado tiempo y recursos. Los métodos alternativos que hacen uso de columnas de marca de tiempo, desencadenadores o consultas complejas suelen afectar al rendimiento y aumentar la complejidad. Lo que se necesita es un flujo de datos modificados confiable y estructurado de forma que los consumidores puedan aplicarlo fácilmente a las representaciones de destino de los datos. La captura de datos modificados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona esta solución.  
  
 El mecanismo de captura de datos modificados de [!INCLUDE[ssDE](../../includes/ssde-md.md)] captura las operaciones de inserción, actualización y eliminación aplicadas a las tablas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y proporciona los detalles de los cambios en un formato relacional fácil de utilizar. Las tablas de cambios utilizadas por la captura de datos modificados contienen las columnas que reflejan la estructura de columnas de las tablas de origen a las que se realiza el seguimiento junto con los metadatos necesarios para entender los cambios que se han producido en cada fila.  
  
> [!NOTE]  
>  Captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="how-change-data-capture-works-in-integration-services"></a>Cómo funciona la captura de datos modificados en Integration Services  
 Un paquete de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] puede recopilar con facilidad los datos modificados en las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para realizar cargas incrementales con eficacia en un almacenamiento de datos. Sin embargo, antes de poder utilizar [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] para cargar los datos modificados, el administrador debe habilitar la captura de datos modificados en la base de datos y en las tablas cuyos cambios se desean capturar. Para obtener más información sobre cómo configurar la captura de datos modificados en una base de datos, vea [Habilitar y deshabilitar la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md).  
  
 Cuando el administrador ha habilitado la captura de datos modificados en la base de datos, es posible crear un paquete que realiza una carga incremental de los datos modificados. El diagrama siguiente muestra los pasos necesarios para crear un paquete de este tipo que realiza una carga incremental desde una sola tabla:  
  
 ![Pasos de creación de un paquete de Change Data Capture](../media/cdc-package-creation.gif "Change Data Capture Package Creation Steps")  
  
 Tal como se muestra en el diagrama anterior, la creación de un paquete que realiza una carga incremental de datos modificados conlleva los pasos siguientes:  
  
 **Paso 1: diseñar el flujo de control**  
 Debe definir las tareas siguientes en el flujo de control del paquete:  
  
-   Calcular la fecha inicial y final `datetime` valores para el intervalo de cambios al origen de datos que desea recuperar.  
  
     Para calcular estos valores, utilice una tarea Ejecutar SQL o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] expresiones con `datetime` funciones. A continuación, almacene estos extremos en variables de paquete para usarlas posteriormente en el paquete.  
  
     **Para obtener más información:**[especificar un intervalo de datos modificados  ](specify-an-interval-of-change-data.md)  
  
-   Determine si están listos los datos modificados para el intervalo seleccionado. Este paso es necesario porque es posible que el proceso de captura asincrónico todavía no haya alcanzado el extremo seleccionado.  
  
     Para determinar si están listos los datos, comience con un contenedor de bucles For para retrasar la ejecución, si es necesario, hasta que estén listos los datos modificados para el intervalo seleccionado. Dentro del contenedor de bucles, utilice una tarea Ejecutar SQL para consultar las tablas de asignación de fecha y hora que se mantienen en la captura de datos modificados. A continuación, utilice una tarea Script que llame al método `Thread.Sleep` u otra tarea Ejecutar SQL con una instrucción `WAITFOR`, con objeto de retrasar la ejecución del paquete temporalmente, si es necesario. También puede utilizar otra tarea Script para registrar una condición de error o un tiempo de espera.  
  
     **Para obtener más información:**[determinar si los datos modificados está preparados  ](determine-whether-the-change-data-is-ready.md)  
  
-   Prepare la cadena de consulta que se utilizará para consultar los datos modificados.  
  
     Use una tarea Script o Ejecutar SQL para ensamblar la instrucción SQL que se usará para consultar si hay cambios.  
  
     **Para obtener más información:**[preparar para consultar los datos modificados  ](prepare-to-query-for-the-change-data.md)  
  
 **Paso 2: configurar la consulta para los datos modificados**  
 Cree la función con valores de tabla que consultará los datos.  
  
 Utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para desarrollar y guardar la consulta.  
  
 **Para obtener más información:**[recuperar y describir datos modificados  ](retrieve-and-understand-the-change-data.md)  
  
 **Paso 3: diseñar el flujo de datos**  
 Debe definir las tareas siguientes en el flujo de datos del paquete:  
  
-   Recupere los datos modificados de las tablas de cambios.  
  
     Para recuperar los datos, utilice un componente de origen para consultar las tablas de cambios con objeto de detectar los cambios comprendidos en el intervalo seleccionado. El origen llama a una función con valores de tabla de Transact-SQL que deberá haber creado previamente.  
  
     **Para obtener más información:**[recuperar y describir datos modificados  ](retrieve-and-understand-the-change-data.md)  
  
-   Divida los cambios en inserciones, actualizaciones y eliminaciones para su procesamiento.  
  
     Para dividir los cambios, utilice una transformación División condicional para dirigir las inserciones, las actualizaciones y las eliminaciones a las distintas salidas con objeto de procesarlas adecuadamente.  
  
     **Para obtener más información:**[procesar inserciones, actualizaciones y eliminaciones  ](process-inserts-updates-and-deletes.md)  
  
-   Aplique las inserciones, eliminaciones y actualizaciones en el destino.  
  
     Con el fin de realizar los cambios en el destino, utilice un componente de destino para aplicar las inserciones en el destino. Asimismo, utilice transformaciones Comando de OLE DB con instrucciones UPDATE y DELETE con parámetros para aplicar las actualizaciones y las eliminaciones en el destino. También puede aplicar las actualizaciones y las eliminaciones mediante componentes de destino para guardar las filas en tablas temporales. A continuación, utilice tareas Ejecutar SQL para realizar operaciones de actualización y eliminación masivas en el destino a partir de las tablas temporales.  
  
     **Para obtener más información:**[aplicar los cambios al destino  ](apply-the-changes-to-the-destination.md)  
  
### <a name="change-data-from-multiple-tables"></a>Datos modificados de varias tablas  
 El proceso descrito en el diagrama y en los pasos anteriores conlleva una carga incremental a partir de una sola tabla. Cuando es preciso realizar una carga incremental a partir de varias tablas, el proceso general es el mismo. Sin embargo, hay que cambiar el diseño del paquete para adaptarlo al procesamiento de varias tablas. Para obtener más información sobre cómo crear un paquete que realiza una carga incremental a partir de varias tablas, vea [Realizar una carga incremental de varias tablas](perform-an-incremental-load-of-multiple-tables.md).  
  
## <a name="samples-of-change-data-capture-packages"></a>Ejemplos de paquetes de captura de datos modificados  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona dos ejemplos que muestran cómo usar cambiar captura de datos en paquetes. Para obtener más información, consulte los temas siguientes:  
  
-   [Léame del ejemplo de captura de datos modificados desde el paquete de la última solicitud](http://go.microsoft.com/fwlink/?LinkId=133507)  
  
-   [Léame del ejemplo de captura de datos de cambio desde el paquete de la última solicitud](http://go.microsoft.com/fwlink/?LinkId=133508)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Especificar un intervalo de datos modificados](specify-an-interval-of-change-data.md)  
  
-   [Determinar si los datos modificados están preparados](determine-whether-the-change-data-is-ready.md)  
  
-   [Preparar para consultar datos modificados](prepare-to-query-for-the-change-data.md)  
  
-   [Crear la función para recuperar los datos modificados](create-the-function-to-retrieve-the-change-data.md)  
  
-   [Recuperar y describir datos modificados](retrieve-and-understand-the-change-data.md)  
  
-   [Procesar inserciones, actualizaciones y eliminaciones](process-inserts-updates-and-deletes.md)  
  
-   [Aplicar los cambios al destino](apply-the-changes-to-the-destination.md)  
  
-   [Realizar una carga incremental de varias tablas](perform-an-incremental-load-of-multiple-tables.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, sobre el [patrón de diseño de SSIS y la carga incremental](http://go.microsoft.com/fwlink/?LinkId=217679), en sqlblog.com  
  
  
