---
title: Utilizar widgets de una visión general para supervisar los servidores y bases de datos de las SQL Operations Studio (preview) | Documentos de Microsoft
description: Obtenga información acerca de los widgets de una visión general de las SQL Operations Studio (preview).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d810e0b5ed89b93ac3d56a12758285fbd297092b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Administrar servidores y bases de datos con los widgets de una visión general de[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Widgets de Insight toman las consultas de Transact-SQL (T-SQL) que se usa para supervisar servidores y bases de datos y los convierte en visualizaciones precisos. 

Visión es personalizables diagramas y gráficos que agregue al servidor y paneles de supervisión de la base de datos. Ver información de un vistazo de los servidores y bases de datos, a continuación, profundizar en los detalles más e iniciar acciones de administración que defina. 

Puede compilar Maravilla servidor y base de datos de administración paneles similares al ejemplo siguiente:

![panel base de datos](media/insight-widgets/database-dashboard.png)


Para saltar en y empezar a crear diferentes tipos de widgets de información, consulte los siguientes tutoriales:

- [Crear un widget de información personalizada](tutorial-build-custom-insight-sql-server.md)
- *Habilitar widgets de información integrada*
   - [Habilitar la información de supervisión de rendimiento](tutorial-qds-sql-server.md)
   - [Habilitar la información de uso del espacio de tabla](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Consultas SQL 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]intenta evitar introducir aún otro usuario de lenguaje o a la sobrecarga de la interfaz por lo que intenta usar T-SQL tanto como sea posible con la configuración mínima de JSON. Configuración de widgets de una perspectiva con T-SQL aprovecha el número innumerables de orígenes de consultas T-SQL útiles que se pueden convertir en detalle widgets existentes.

Widgets de una perspectiva se componen de uno o dos consultas de T-SQL:
* *Consulta de widget de Insight* es obligatorio, y es la consulta que devuelve los datos que aparecen en el widget.
* *Consulta de detalles de una perspectiva* es necesario sólo si va a crear una página de detalles de una visión general.

Una consulta de widget de una perspectiva define un conjunto de datos que representa un recuento o un gráfico. Consulta de detalles de información se utiliza para mostrar información de detalle de información relevante en un formato tabular en el panel de detalles de una visión general. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]ejecuta consultas de widget de una visión general y se asigna el conjunto de resultados de consulta al conjunto de datos de un gráfico, a continuación, lo representa. Cuando los usuarios abran los detalles de una idea, ejecuta la consulta de detalles de una visión general e imprime el resultado en una vista de cuadrícula en el cuadro de diálogo.

La idea básica es escribir una consulta de T-SQL de una manera para que se pueda usar como un conjunto de datos de un recuento, el gráfico y el widget de gráfico. 

## <a name="summary"></a>Resumen

La consulta de T-SQL y su conjunto de resultados determinan el comportamiento de widget de información. Escribir una consulta para un tipo de gráfico o asignación de un tipo de gráfico adecuado para la consulta existente es el aspecto clave para generar un widget de información eficaces.



## <a name="additional-resources"></a>Recursos adicionales
- [Editor de consultas](tutorial-sql-editor.md)

