---
title: Filtros de combinación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- publications [SQL Server replication], join filters
- merge replication join filters [SQL Server replication]
- join filters
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f95392c4805df824418f3f9682f2f53b9589ea9c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010513"
---
# <a name="join-filters"></a>filtros de combinación
  Un filtro de combinación permite filtrar una tabla en función de cómo se haya filtrado una tabla relacionada en la publicación. Normalmente, una tabla primaria se filtra utilizando un filtro con parámetros; por tanto, los filtros de combinación se definen de manera muy similar a como se define una combinación entre tablas. Los filtros de combinación amplían el filtro con parámetros de modo que los datos de las tablas relacionadas solo se replican si coinciden con la cláusula del filtro de combinación.  
  
 Normalmente, los filtros de combinación siguen las relaciones entre clave principal y clave externa definidas para las tablas en las que se aplican, aunque no se limitan estrictamente a dichas relaciones. Un filtro de combinación puede estar basado en cualquier lógica que compare datos relacionados en dos tablas.  
  
 Considere las siguientes tablas de la base de datos de ejemplo [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] , que tienen relaciones de clave principal a clave externa:  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 Estas tablas se podrían utilizar en una aplicación para dar apoyo al personal de ventas móvil, pero es necesario filtrarlas para que cada una de las personas de la tabla **HumanResources.Employee** reciba solo los datos de los pedidos de sus clientes.  
  
 El primer paso es definir un filtro con parámetros en la tabla primaria, que en este ejemplo es la tabla **HumanResources.Employee** . Esta tabla incluye la columna **LoginID**, que contiene el inicio de sesión de cada empleado en la forma *dominio\inicioDeSesión*. Para filtrar esta tabla con el objeto de que cada empleado reciba únicamente los datos pertinentes, especifique la siguiente cláusula de filtro:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Este filtro asegura que cada suscripción de empleado contenga solamente los datos de la tabla **HumanResources.Employee** que sean relevantes para dicho empleado (que en este caso es una sola fila). Para obtener más información, consulte [Filtros de fila con parámetros](parameterized-filters-parameterized-row-filters.md).  
  
 El siguiente paso es extender este filtro a cada una de las tablas relacionadas, utilizando una sintaxis similar a la que se utiliza para especificar una combinación entre dos tablas. La cláusula de este primer filtro de combinación es:  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 Esto asegura que la suscripción contenga solo los datos relevantes para cada vendedor. La cláusula del segundo filtro de combinación es:  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 Esto asegura que la suscripción contenga solo los datos detallados relacionados con los datos del pedido de cada vendedor. En este ejemplo se muestra una única tabla que se ha combinado en cada punto; también es posible combinar más de una tabla en cada punto.  
  
 Los filtros de combinación se pueden agregar de uno en uno mediante el Asistente para nueva publicación y el cuadro de diálogo **Propiedades de la publicación** , y también mediante programación. También se pueden generar automáticamente a través del Asistente para nueva publicación: se especifica un filtro de fila para una tabla y los filtros de combinación se aplican a todas las tablas relacionadas. Para obtener más información, vea [Definir y modificar un filtro de combinación entre artículos de mezcla](../publish/define-and-modify-a-join-filter-between-merge-articles.md), [Generar automáticamente un conjunto de filtros de combinación entre artículos de mezcla &#40;SQL Server Management Studio&#41;](../publish/automatically-generate-join-filters-between-merge-articles.md) y [Definir un artículo](../publish/define-an-article.md).  
  
## <a name="optimizing-join-filter-performance"></a>Optimizar el rendimiento de los filtros de combinación  
 El rendimiento de los filtros de combinación se puede optimizar siguiendo estas instrucciones:  
  
-   Limite el número de tablas de la jerarquía del filtro de combinación.  
  
     Los filtros de combinación pueden implicar un número ilimitado de tablas, pero los filtros con un gran número de tablas pueden producir un efecto significativo en el rendimiento durante el proceso de mezcla. Si va a generar filtros de combinación de cinco tablas o más, considere otras soluciones, como no filtrar tablas pequeñas, que no estén sometidas a cambios o que sean principalmente tablas de búsqueda. Utilice filtros combinados solo entre tablas que deben particionarse entre las suscripciones.  
  
-   Establezca la opción **join unique key** en **True** donde corresponda.  
  
     El proceso de mezcla dispone de optimizaciones de rendimiento especiales si la columna combinada en el elemento primario es única. Si la condición de combinación se basa en una columna única, establezca la opción **join unique key** para el filtro de combinación. Para obtener información sobre el modo de establecer esta opción, vea los temas de procedimientos enumerados en la sección anterior.  
  
-   Asegúrese de que las columnas a las que se hace referencia en los filtros de combinación están indizadas.  
  
     Si las columnas a las que se hace referencia en el filtro están indizadas, la replicación podrá procesar los filtros con más eficacia.  
  
-   No cree filtros de fila que se comporten como filtros de combinación.  
  
     Es posible crear filtros de fila que se comporten como filtros de combinación utilizando una subconsulta en una cláusula WHERE como la siguiente:  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     Se recomienda encarecidamente que todas las lógicas similares se expresen en un filtro de combinación en lugar de una subconsulta. Si la aplicación requiere que un filtro de fila utilice una subconsulta, asegúrese de que la subconsulta solo hace referencia a los datos de búsqueda que no cambian.  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar datos publicados para la replicación de mezcla](filter-published-data-for-merge-replication.md)   
 [Filtros de fila con parámetros](parameterized-filters-parameterized-row-filters.md)  
  
  
