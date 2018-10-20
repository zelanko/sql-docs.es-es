---
title: Usar los widgets de datos para supervisar servidores y bases de datos de Azure Data Studio | Microsoft Docs
description: Obtenga información acerca de los widgets de datos en Azure Data Studio.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d669b72aadb9fe1ea2ec61c2059a1d932ee52d4d
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356336"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Administrar servidores y bases de datos con los widgets de datos en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Widgets de datos realizar las consultas de Transact-SQL (T-SQL) que se utiliza para supervisar los servidores y bases de datos y convertirlos en visualizaciones muy precisos. 

Insights son personalizables diagramas y gráficos que agrega al servidor y los paneles de supervisión de la base de datos. Ver información de un vistazo de los servidores y bases de datos, a continuación, profundizar en más detalles e iniciar acciones de administración que defina. 

Puede crear increíbles servidor y base de datos de administración paneles similares al ejemplo siguiente:

![panel de la base de datos](media/insight-widgets/database-dashboard.png)


Para dar el salto y empezar a crear diferentes tipos de widgets de datos, consulte los siguientes tutoriales:

- [Crear un widget de datos personalizados](tutorial-build-custom-insight-sql-server.md)
- *Habilitar los widgets de datos integrados*
   - [Habilitar la información de supervisión de rendimiento](tutorial-qds-sql-server.md)
   - [Habilitar la información de uso del espacio de tabla](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Consultas SQL 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] intenta evitar introducir aún otro lenguaje o con mucha actividad de usuario de la interfaz por lo que intenta usar T-SQL tanto como sea posible con muy poca configuración de JSON. Configuración de widgets de datos con Transact-SQL aprovecha el número de orígenes existentes de las consultas de Transact-SQL útiles que pueden convertirse en widgets perspicaces innumerables.

Widgets de datos se componen de uno o dos consultas de T-SQL:
* *Consulta de widget Insight* es obligatorio, y es la consulta que devuelve los datos que aparecen en el widget.
* *Consulta de detalles de Insight* es necesario sólo si va a crear una página de detalles de la información.

Una consulta de widget de una perspectiva define un conjunto de datos que representa un recuento o un gráfico. Consulta de detalles de la información se usa para mostrar información de detalle de información relevante en formato tabular en el panel de detalles de la información. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] ejecuta consultas de widget de insight y asigna el conjunto de resultados de consulta al conjunto de datos de un gráfico, a continuación, lo representa. Cuando los usuarios abren los detalles de una recomendación, ejecuta la consulta de detalles de insight e imprime el resultado en una vista de cuadrícula en el cuadro de diálogo.

La idea básica consiste en escribir una consulta de Transact-SQL en una forma por lo que puede usarse como un conjunto de datos de un número y gráfico widget de gráfico. 

## <a name="summary"></a>Resumen

La consulta de Transact-SQL y su conjunto de resultados determinan el comportamiento del widget de información. Escribir una consulta para un tipo de gráfico o la asignación de un tipo de gráfico adecuado para la consulta existente es el aspecto clave para crear un widget de información eficaces.



## <a name="additional-resources"></a>Recursos adicionales
- [Editor de consultas](tutorial-sql-editor.md)

