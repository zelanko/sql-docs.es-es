---
title: Biblioteca de funciones de R de olapR
description: Introducción a la biblioteca de funciones de olapR en SQL Server 2016 R Services y SQL Server Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117418"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (biblioteca de R en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** es una biblioteca de Microsoft de funciones de R utilizadas para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. Las funciones no admiten todas las operaciones MDX, pero puede crear consultas que segmenten, desmenucen, obtengan detalles, acumulen y dinamicen en las dimensiones. 

Este paquete no se ha cargado previamente en una sesión de R. Ejecute el siguiente comando para cargar la biblioteca.

```R
library(olapR)
```

Puede usar esta biblioteca en las conexiones a un cubo OLAP de Analysis Services en todas las versiones compatibles de SQL Server. En este momento no se admiten las conexiones a un modelo tabular.

## <a name="package-version"></a>Versión del paquete

La versión actual es 1.0.0 en todos los productos solo de Windows y descargas que proporcionan la biblioteca.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca de **olapr** se distribuye en varios productos de Microsoft, pero el uso es el mismo, se obtenga la biblioteca en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

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

<sup>1</sup> integración de R es opcional en SQL Server. La biblioteca de olapr se instalará cuando agregue la característica Machine Learning o de R durante la configuración de la máquina virtual.


## <a name="see-also"></a>Consulte también

[Cómo crear consultas MDX con olapR](how-to-create-mdx-queries-using-olapr.md)
