---
title: Almacenar en caché conjuntos de datos compartidos (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4acb1bbe-1c04-4979-b893-dc1b1c5039b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8fcb3e8c423e629a33a0c173e3264ee11ee178f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104180"
---
# <a name="cache-shared-datasets-ssrs"></a>Almacenar en caché conjuntos de datos compartidos (SSRS)
  Los resultados de las consultas para un conjunto de datos compartido se pueden copiar en una memoria caché para proporcionar datos coherentes a varios informes y mejorar el tiempo de respuesta de la consulta del conjunto de datos. Al igual que los informes, puede configurar un conjunto de datos compartido que se va a almacenar en memoria caché al usarse por primera vez o especificando una programación.  
  
 Un conjunto de datos compartido puede estar incluido en varios informes o como parte de las definiciones de componentes. Al almacenar en memoria caché el conjunto de datos compartido, proporciona un conjunto coherente de datos para todos los informes que lo utilizan y también reduce el número de veces que la consulta del conjunto de datos se ejecuta con el origen de datos externo.  
  
 La siguiente lista proporciona ejemplos de cuándo almacenar en memoria caché un conjunto de datos compartido:  
  
-   La consulta tarda bastante tiempo en ejecutarse.  
  
-   La consulta acepta parámetros, pero el número de combinaciones de parámetros es pequeño la mayor parte del tiempo. Cada combinación crea resultados de la consulta almacenados en memoria caché.  
  
-   La consulta se ejecuta en momentos predecibles del día, semana o mes.  
  
-   La consulta se ejecuta como resultado de una referencia del conjunto de datos compartido en un informe que se entrega a través del correo electrónico, donde es probable que un número grande de personas haga clic en el vínculo en un breve intervalo de tiempo.  
  
-   La siguiente lista proporciona ejemplos de cuándo no almacenar en memoria caché un conjunto de datos compartido:  
  
-   Los resultados de la consulta siempre deben incluir los datos más recientes.  
  
-   La consulta se ejecuta rápidamente.  
  
-   La consulta se ejecuta con poca frecuencia.  
  
-   La consulta acepta parámetros, el número de combinaciones de parámetros es grande y ninguna combinación es más probable que otra.  
  
-   El origen de datos en el que se basa el conjunto de datos compartido tiene credenciales integradas de Windows o hay que proporcionarlas.  
  
-   El filtro del conjunto de datos compartido o la consulta contienen una expresión con una referencia al usuario de la colección global.  
  
 Si un usuario elige valores para los parámetros de informe que difieren de los valores predeterminados que están especificados para el conjunto de resultados almacenado en memoria caché, la consulta del conjunto de datos se ejecuta activamente y los resultados almacenados en la memoria caché no se utilizan para esa consulta.  
  
## <a name="caching-shared-datasets"></a>Almacenamiento en caché de conjuntos de datos compartido  
 Para habilitar el almacenamiento en caché para un conjunto de datos compartido, debe seleccionar la opción de memoria caché en el conjunto de datos compartido. Una vez habilitado el almacenamiento en caché, los resultados de la consulta para un conjunto de datos compartido se copian en la memoria caché cuando se usan por primera vez. Si el conjunto de datos compartido tiene parámetros, cada combinación de parámetros crea una nueva entrada en la memoria caché.  
  
 Mientras los resultados de la consulta para una combinación de parámetros concreta estén en la memoria caché, cada informe que se inicie para procesarse y que incluya una referencia al conjunto de datos compartido con esos valores de parámetros utilizará los datos de la memoria caché.  
  
 Puede especificar cuánto tiempo se mantendrán los datos en la memoria caché antes de que expiren. Para más información, vea [Página de almacenamiento en caché, conjuntos de datos compartidos &#40;Administrador de informes&#41;](../caching-page-shared-datasets-report-manager.md).  
  
## <a name="preloading-the-cache"></a>Cargar previamente la memoria caché  
 Puede cargar previamente la memoria caché creando un plan de actualización de caché. Con un plan de actualización, puede especificar la frecuencia de la actualización de la memoria caché utilizando una programación específica de los elementos o una programación compartida. Para evitar varias entradas en la memoria caché para el mismo elemento, la programación que especifique debería permitir suficiente tiempo para el procesamiento de las consultas en el origen de datos externo. Por ejemplo, si la consulta tarda 20 minutos en ejecutarse, la programación de la actualización debería ser mayor de 20 minutos. Para obtener más información, vea [Schedules](../subscriptions/schedules.md).  
  
 Para crear un plan de actualización de caché para un conjunto de datos compartido, se aplican las siguientes condiciones.  
  
-   El conjunto de datos compartido se debe habilitar para el almacenamiento en memoria caché.  
  
-   El origen de datos compartido del que el conjunto de datos compartido depende no puede utilizar credenciales integradas de Windows ni credenciales que deban proporcionarse.  
  
-   Si el conjunto de datos compartido tiene parámetros, debe especificar valores predeterminados estáticos para cada parámetro que no esté marcado como de solo lectura. Los parámetros de solo lectura siempre utilizarán el valor predeterminado. Si desea almacenar en memoria caché un conjunto de datos compartido para varias combinaciones de parámetros, debe crear un plan de actualización de caché independiente para cada combinación de valores. Los parámetros no pueden contener referencias a otros conjuntos de datos.  
  
-   Cada plan de actualización de caché está asociado solo a un conjunto de datos compartido o informe.  
  
-   Debe tener los permisos ReadPolicy y UpdatePolicy en el conjunto de datos compartido.  
  
 Los planes de actualización de memoria caché se aplican a los conjuntos de datos compartidos y a los informes. Para más información, vea [Opciones de actualización de memoria caché &#40;Administrador de informes&#41;](../cache-refresh-options-report-manager.md).  
  
## <a name="conditions-that-cause-cache-expiration"></a>Situaciones que pueden provocar la expiración de la memoria caché  
 Las siguientes condiciones pueden hacer que una memoria caché del conjunto de datos compartido deje de ser válida.  
  
-   Una condición de programación expira. La memoria caché expira o llega la fecha de expiración.  
  
-   Se elimina una programación compartida.  
  
-   Cambios en una programación compartida. Las programaciones compartidas se pueden pausar, lo que también afecta al momento en que una memoria caché expira.  
  
-   La definición de la consulta para el conjunto de datos compartido cambia.  
  
-   Las credenciales del origen de datos compartido del que el conjunto de datos compartido depende cambian.  
  
-   Las opciones de memoria caché para el conjunto de datos compartido cambian.  
  
-   Los valores predeterminados para los parámetros de solo lectura para el conjunto de datos compartido cambian.  
  
-   Los filtros que forman parte de la definición del conjunto de datos compartido cambian.  
  
-   El conjunto de datos compartido se elimina del servidor de informes. Cuando se elimina un conjunto de datos compartido, también se eliminan las copias en caché asociadas y los planes de actualización de memoria caché.  
  
 Las actualizaciones de los planes de actualización de memoria caché para los conjuntos de datos compartidos no afectan a los informes que ya se estén procesando. La actualización de un plan de actualización de caché solo afecta a las versiones futuras de los informes que hagan referencia al conjunto de datos compartido.  
  
## <a name="see-also"></a>Consulte también  
 [Administración de conjuntos de datos compartidos](../report-data/manage-shared-datasets.md)  
  
  
