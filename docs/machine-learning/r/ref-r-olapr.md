---
title: Paquete olapR de R
description: OlapR es un paquete de R de Microsoft que se usa para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. Las funciones no admiten todas las operaciones MDX, pero puede crear consultas que segmenten, desmenucen, obtengan detalles, acumulen y dinamicen en las dimensiones. El paquete se incluye en SQL Server Machine Learning Services y en SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 844489b4c9f3e0e92848ebb1c9cb3b725ac5fedd
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406168"
---
# <a name="olapr-r-package-in-sql-server-machine-learning-services"></a>OlapR (paquete de R en SQL Server Machine Learning Services)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**OlapR** es un paquete de R de Microsoft que se usa para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. Las funciones no admiten todas las operaciones MDX, pero puede crear consultas que segmenten, desmenucen, obtengan detalles, acumulen y dinamicen en las dimensiones. El paquete se incluye en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) y en [SQL Server 2016 R Services](sql-server-r-services.md).

Puede usar este paquete en las conexiones a un cubo OLAP de Analysis Services en todas las versiones compatibles de SQL Server. En este momento no se admiten las conexiones a un modelo tabular.

## <a name="load-package"></a>Carga de paquete

El paquete **olapR** no se ha cargado previamente en una sesión de R. Ejecute el siguiente comando para cargar el paquete.

```R
library(olapR)
```

## <a name="package-version"></a>Versión del paquete

La versión actual es 1.0.0 en todos los productos solo de Windows y descargas que proporcionan el paquete.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El paquete **olapr** se distribuye en varios productos de Microsoft, pero el uso es el mismo independientemente de si se obtiene el paquete en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="availability-and-location"></a>Disponibilidad y ubicación

Este paquete se proporciona en los siguientes productos, así como en varias imágenes de máquina virtual en Azure. La ubicación del paquete varía en consecuencia.

Producto | Location |
--------|----------|
SQL Server Machine Learning Services (con la integración de R) | C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Archivos de programa\Microsoft\ R_SERVER \library |
Cliente de Microsoft R | C:\Archivos de programa\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (en Azure) | C:\Archivos de programa\Microsoft\R Client\R_SERVER\library |
SQL Server Virtual Machine (en Azure) <sup>1</sup> | C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> integración de R es opcional en SQL Server. El paquete olapr se instalará cuando agregue la característica Machine Learning o de R durante la configuración de la máquina virtual.


## <a name="see-also"></a>Consulte también

[Cómo crear consultas MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
