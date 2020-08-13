---
title: Trabajo con conjuntos de resultados
description: Obtenga información sobre cómo trabajar con datos mediante conjuntos de resultados en el controlador JDBC para SQL Server en estas aplicaciones de ejemplo.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82618ee27e1aa32716fe4b4d3817ff0128baebab
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921031"
---
# <a name="working-with-result-sets"></a>Trabajo con conjuntos de resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Si trabaja con los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uno de los métodos para manipular los datos consiste en usar un conjunto de resultados. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso de conjuntos de resultados mediante el objeto [SQLServerResultSet](reference/sqlserverresultset-class.md). Si usa el objeto SQLServerResultSet, puede recuperar los datos devueltos desde una instrucción SQL o un procedimiento almacenado, actualizar los datos según sea necesario y luego volver a almacenarlos en la base de datos.

Además, el objeto SQLServerResultSet proporciona métodos para desplazarse por las filas de datos, obtener o configurar los datos que contiene y establecer varios niveles de sensibilidad a los cambios en la base de datos subyacente.

> [!NOTE]
> Para obtener más información sobre la administración de los conjuntos de resultados, incluida la sensibilidad a los cambios, consulte [Administrar conjuntos de resultados con el controlador JDBC](managing-result-sets-with-the-jdbc-driver.md).

En los temas de esta sección se describen las distintas formas en que puede usar un conjunto de resultados para manipular los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="in-this-section"></a>En esta sección

| Tema                                                                     | Descripción                                                                                                                                                                                          |
| ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Recuperación de ejemplo de datos de conjunto de resultados](retrieving-result-set-data-sample.md) | Se describe cómo usar un conjunto de resultados para recuperar y mostrar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                         |
| [Modificación de ejemplo de datos de conjunto de resultados](modifying-result-set-data-sample.md)   | Se describe cómo usar un conjunto de resultados para insertar, recuperar y modificar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                      |
| [Almacenamiento en caché de ejemplo de datos de conjunto de resultados](caching-result-set-data-sample.md)       | Se describe cómo usar un conjunto de resultados para recuperar grandes cantidades de datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo controlar el modo en que los datos se almacenan en la memoria caché del cliente. |

## <a name="see-also"></a>Consulte también

[Aplicaciones de ejemplo del controlador JDBC](sample-jdbc-driver-applications.md)
